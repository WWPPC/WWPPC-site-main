<script setup lang="ts">
import WaitCover from '#/common/WaitCover.vue';
import { AnimateInContainer, PairedGridContainer, TitledCollapsibleContainer, TitledCutCornerContainer } from '#/containers';
import { InputButton, InputTextArea, InputTextBox, InputDropdown, InputCopyButton } from '#/inputs';
import AccountTeamUserDisp from '#/common-components/account/AccountTeamUserDisp.vue';
import { onMounted, ref, watch } from 'vue';
import { globalModal, ModalMode } from '#/modal';
import { useAccountManager, gradeMaps, experienceMaps, languageMaps } from '#/modules/AccountManager';
import { useRoute } from 'vue-router';

const route = useRoute();
const modal = globalModal();
const accountManager = useAccountManager();

const loading = ref(true);
onMounted(async () => {
    loading.value = true;
    await accountManager.updateOwnUserData();
    loading.value = false;
    usernameNotEditable.value = accountManager.username;
    gradeInput.value = accountManager.grade?.toString();
    experienceInput.value = accountManager.experience?.toString();
    joinCodeNotEditable.value = accountManager.teamJoinCode ?? '';
    emailNotEditable.value = accountManager.email;
});

// prevent username being overwritten
const usernameNotEditable = ref('');
const emailNotEditable = ref('');
const joinCodeNotEditable = ref('');
watch(() => accountManager.username, () => usernameNotEditable.value = accountManager.username);
watch(() => accountManager.teamJoinCode, () => joinCodeNotEditable.value = accountManager.teamJoinCode ?? '');
watch(() => accountManager.email, () => emailNotEditable.value = accountManager.email);

// oops
const gradeInput = ref('');
const experienceInput = ref('');
const languagesInput = ref<string[]>([]);
watch(gradeInput, () => accountManager.grade = Number(gradeInput.value));
watch(experienceInput, () => accountManager.experience = Number(experienceInput.value));
watch(languagesInput, () => accountManager.languages = languagesInput.value);
watch(() => accountManager.grade, () => gradeInput.value = accountManager.grade?.toString());
watch(() => accountManager.experience, () => experienceInput.value = accountManager.experience?.toString());
watch(() => accountManager.languages, () => languagesInput.value = accountManager.languages);

const remainingBioCharacters = ref(2048);
const remainingBioCharacters2 = ref(1024);
watch(() => accountManager.bio, () => remainingBioCharacters.value = 2048 - accountManager.bio?.length);
watch(() => accountManager.teamBio, () => remainingBioCharacters2.value = 1024 - accountManager.teamBio?.length);

const showWriteDataWait = ref(false);
const writeData = async () => {
    showWriteDataWait.value = true;
    // artificial wait
    await new Promise((resolve) => setTimeout(resolve, 500));
    const res = await accountManager.writeUserData();
    if (res != AccountOpResult.SUCCESS) modal.showModal({ title: 'Write data failed', content: getAccountOpMessage(res), color: 'red' });
    showWriteDataWait.value = false;
};

// teams
const joinTeamCode = ref('');
const showWriteTeamDataWait = ref(false);
const writeTeamData = async () => {
    showWriteTeamDataWait.value = true;
    // artificial wait
    await new Promise((resolve) => setTimeout(resolve, 500));
    const res = await accountManager.writeTeamData();
    if (res != TeamOpResult.SUCCESS) modal.showModal({ title: 'Write data failed', content: getTeamOpMessage(res), color: 'red' });
    showWriteTeamDataWait.value = false;
};
const joinTeam = async () => {
    showWriteTeamDataWait.value = true;
    if (joinTeamCode.value.length != 6) return;
    const res = await accountManager.joinTeam(joinTeamCode.value);
    if (res == TeamOpResult.NOT_EXISTS) modal.showModal({ title: 'Invalid join code', content: 'The join code is invalid. Verify your join code is correct, then try again.', color: 'yellow' });
    else if (res != TeamOpResult.SUCCESS) modal.showModal({ title: 'Could not join team', content: getTeamOpMessage(res), color: 'red' });
    await accountManager.updateOwnUserData();
    showWriteTeamDataWait.value = false;
};
const leaveTeam = async () => {
    const confirmation = await modal.showModal({ title: 'Leave team?', content: 'You are about to leave the team. Are you sure?', mode: ModalMode.CONFIRM, color: 'yellow' }).result;
    if (!confirmation) return;
    showWriteTeamDataWait.value = true;
    if (accountManager.username == accountManager.team) return;
    const res = await accountManager.leaveTeam();
    if (res != TeamOpResult.SUCCESS) modal.showModal({ title: 'Could not leave team', content: getTeamOpMessage(res), color: 'red' });
    await accountManager.updateOwnUserData();
    showWriteTeamDataWait.value = false;
};

const teamCodeType = ref<'text' | 'password'>('password');
const onCodeMouseEnter = () => {
    teamCodeType.value = 'text';
};
const onCodeMouseLeave = () => {
    teamCodeType.value = 'password';
};
onMounted(() => {
    document.addEventListener('blur', () => teamCodeType.value = 'password');
});

// danger buttons
const showCredWait = ref(false);
const currentPasswordInput = ref('');
const newPasswordInput = ref('');
const changePasswordEnabled = ref(false);
const changePassword = async () => {
    const currPassword = currentPasswordInput.value;
    clearDangerButtons();
    const newPassword = await modal.showModal({
        title: 'Change Password',
        content: 'Enter your new password:',
        mode: ModalMode.QUERY,
        inputType: 'password'
    }).result;
    // also handles "cancel" case
    if (typeof newPassword != 'string' || newPassword.trim() == '') return;
    if (newPassword.length >= 1024) {
        modal.showModal({
            title: 'Password Too Long!',
            content: 'Wow, that\'s a <i>REALLY</i> long password! However, please make it less than 1024 characters!',
            color: 'red'
        });
        return;
    }
    let newPassword2 = await modal.showModal({
        title: 'Change Password',
        content: 'Enter the password again:',
        mode: ModalMode.QUERY,
        inputType: 'password'
    }).result;
    if (typeof newPassword2 != 'string' || newPassword2.trim() == '') return;
    while (newPassword2 !== newPassword) {
        newPassword2 = await modal.showModal({
            title: 'Change Password',
            content: 'Make sure you entered the same password.<br>Enter the password again:',
            mode: ModalMode.QUERY,
            inputType: 'password'
        }).result;
        if (typeof newPassword2 != 'string' || newPassword2.trim() == '') return;
    }
    let spam = true;
    async function modalSpam() {
        while (spam) {
            await modal.showModal({
                title: 'Change Password',
                content: 'Please wait...',
            }).result;
        }
    }
    modalSpam();
    const res = await accountManager.changePassword(currPassword, newPassword);
    spam = false;
    modal.cancelAllModals();
    if (res == 0) window.location.reload();
    else modal.showModal({ title: 'Could not change password:', content: getAccountOpMessage(res), color: 'red' });
};
const deleteAccount = async () => {
    const currPassword = currentPasswordInput.value;
    clearDangerButtons();
    if (await modal.showModal({
        title: 'Delete Account',
        content: '',
        color: 'red',
        mode: ModalMode.CONFIRM
    }).result === false) return;
    if (await modal.showModal({
        title: 'Delete Account',
        content: '<span style="color: red;">Are you SURE that you want to <b>DELETE</b> your account?</span>',
        color: 'red',
        mode: ModalMode.CONFIRM
    }).result === false) return;
    if (await modal.showModal({
        title: 'Delete Account',
        content: '<span style="color: red;">This will <b>PERMANENTLY DELETE ALL DATA</b>, including <b>TEAMS</b>!</span>',
        color: 'red',
        mode: ModalMode.CONFIRM
    }).result === false) return;
    let password2 = await modal.showModal({
        title: 'Delete Account',
        content: '<span style="color: red;">Enter your password to confirm <b>PERMANENT DELETION</b> of your account</span>',
        color: 'red',
        mode: ModalMode.QUERY,
        inputType: 'password'
    }).result;
    if (password2 === null) return;
    while (password2 !== currPassword) {
        password2 = await modal.showModal({
            title: 'Delete Account',
            content: '<span style="color: red;">Passwords do not match.<br>Enter your password to confirm <b>PERMANENT DELETION</b> of your account</span>',
            color: 'red',
            mode: ModalMode.QUERY,
            inputType: 'password'
        }).result;
        if (password2 === null) return;
    }
    let spam = true;
    async function modalSpam() {
        while (spam) {
            await modal.showModal({
                title: 'Delete Account',
                content: 'Please wait...',
            }).result;
        }
    }
    modalSpam();
    const res = await accountManager.deleteAccount(currPassword);
    spam = false;
    await modal.cancelAllModals();
    if (res == 0) window.location.reload();
    else modal.showModal({ title: 'Could not delete account:', content: getAccountOpMessage(res), color: 'red' });
};
const clearDangerButtons = () => {
    currentPasswordInput.value = '';
    newPasswordInput.value = '';
    changePasswordEnabled.value = false;
};
onMounted(clearDangerButtons);
</script>

<template>
    <AnimateInContainer type="slideUp" :delay=100>
        <TitledCutCornerContainer title="Profile" hover-animation="lift">
            <form action="javascript:void(0)" @submit=writeData>
                <PairedGridContainer width=100%>
                    <span>Display Name:</span>
                    <InputTextBox v-model=accountManager.displayName maxlength="32" width="var(--fwidth)" title="Name used in profile, contests, etc." required></InputTextBox>
                    <span>Name:</span>
                    <span class="nowrap">
                        <InputTextBox v-model=accountManager.firstName maxlength="32" width="var(--hwidth)" title="First name" required></InputTextBox>
                        <InputTextBox v-model=accountManager.lastName maxlength="32" width="var(--hwidth)" title="Last name" required></InputTextBox>
                    </span>
                    <span>School:</span>
                    <InputTextBox v-model=accountManager.school maxlength="64" width="var(--fwidth)" title="Your school name" required></InputTextBox>
                    <span>Grade/Experience:</span>
                    <span class="nowrap">
                        <InputDropdown v-model=gradeInput width="var(--hwidth)" :items="gradeMaps" title="Your current grade level" required></InputDropdown>
                        <InputDropdown v-model=experienceInput width="var(--hwidth)" :items="experienceMaps" title="Your experience level with competitive programming" required></InputDropdown>
                    </span>
                    <span>Known Languages:<br>(Use CTRL/SHIFT)</span>
                    <InputDropdown v-model=languagesInput width="var(--fwidth)" :items="languageMaps" title="What programming languages have you used in contest?" height="80px" multiple></InputDropdown>
                    <span>Biography<br>({{ remainingBioCharacters }} chars):</span>
                    <InputTextArea v-model=accountManager.bio width="var(--fwidth)" min-height="2em" height="4em" max-height="20em" maxlength="2048" placeholder="Describe yourself in a few short sentences!" resize="vertical"></InputTextArea>
                </PairedGridContainer>
                <InputButton class="profileSaveButton" type="submit" v-if=accountManager.unsavedChanges text="Save" color="yellow" glitch-on-mount></InputButton>
            </form>
            <WaitCover text="Please wait..." :show="(showWriteDataWait || loading) && route.query.ignore_server === undefined"></WaitCover>
        </TitledCutCornerContainer>
    </AnimateInContainer>
    <AnimateInContainer type="slideUp" :delay=200>
        <TitledCutCornerContainer title="Team" hover-animation="lift">
            <div v-if="accountManager.team === accountManager.username && accountManager.teamMembers.length <= 1">
                <div class="profileTeamSection">
                    <h3>Join a team!</h3>
                    <span class="nowrap">
                        <InputTextBox v-model=joinTeamCode title="Ask team creator for join code!" placeholder="Join code" maxlength="6"></InputTextBox>
                        <InputButton text="Join" :disabled="joinTeamCode.length != 6" @click=joinTeam></InputButton>
                    </span>
                    <br>
                    <i>Joining will sync your registrations to the team</i>
                </div>
                <p>OR</p>
            </div>
            <div class="profileTeamSection">
                <h3>Your Team</h3>
                <div class="profileTeamGrid">
                    <div class="profileTeamList">
                        <AccountTeamUserDisp v-for="user in accountManager.teamMembers" :key="user" :user="user" :team="accountManager.team" allow-kick></AccountTeamUserDisp>
                    </div>
                    <form action="javascript:void(0)" @submit=writeTeamData>
                        <PairedGridContainer width="100%">
                            <span>Team Name:</span>
                            <InputTextBox v-model=accountManager.teamName maxlength="32" width="var(--fwidth)" title="Collective team name" placeholder="Team Name"></InputTextBox>
                            <span>Biography<br>({{ remainingBioCharacters2 }} chars):</span>
                            <InputTextArea v-model=accountManager.teamBio width="var(--fwidth)" min-height="2em" height="4em" max-height="20em" maxlength="1024" placeholder="Describe your team in a few short sentences!" resize="vertical"></InputTextArea>
                        </PairedGridContainer>
                        <InputButton class="profileSaveButton" type="submit" v-if=accountManager.unsavedTeamChanges text="Save" color="yellow" glitch-on-mount></InputButton>
                    </form>
                </div>
            </div>
            <div class="profileTeamSection">
                <span class="nowrap">
                    <span>Join Code:</span>
                    <InputTextBox v-model=joinCodeNotEditable :type=teamCodeType disabled @mouseenter="onCodeMouseEnter" @mouseleave="onCodeMouseLeave"></InputTextBox>
                    <InputCopyButton :value="joinCodeNotEditable ?? ''"></InputCopyButton>
                </span>
            </div>
            <div class="profileTeamSection" v-if="accountManager.team !== accountManager.username">
                <InputButton text="Leave Team" color="red" glitch-on-mount @click=leaveTeam></InputButton>
            </div>
            <WaitCover text="Please wait..." :show="(showWriteTeamDataWait || loading) && route.query.ignore_server === undefined"></WaitCover>
        </TitledCutCornerContainer>
    </AnimateInContainer>
    <AnimateInContainer type="slideUp" :delay=300>
        <TitledCutCornerContainer title="Account" hover-animation="lift">
            <PairedGridContainer>
                <span>Username:</span>
                <InputTextBox v-model=usernameNotEditable width="var(--fwidth)" title="Your unique username (you cannot edit this)" disabled></InputTextBox>
                <span>Email:</span>
                <InputTextBox v-model=emailNotEditable width="var(--fwidth)" title="Email used to update you on contests, password changes, etc. (you cannot edit this)" disabled></InputTextBox>
            </PairedGridContainer>
            <br>
            <TitledCollapsibleContainer title="Danger buttons" font-size="var(--font-medium)" border-color="red" @click="clearDangerButtons" start-collapsed>
                <!-- useless form -->
                <form class="profileDangerButtons" action="javascript:void(0)">
                    <div style="text-align: right; align-content: center; font-size: var(--font-18);">Enter password:</div>
                    <InputTextBox type="password" v-model=currentPasswordInput placeholder="Current password"></InputTextBox>
                    <InputButton text="CHANGE PASSWORD" color="red" @click="changePassword" :disabled="currentPasswordInput.length == 0"></InputButton>
                    <InputButton text="DELETE ACCOUNT" color="red" @click="deleteAccount" :disabled="currentPasswordInput.length == 0"></InputButton>
                </form>
            </TitledCollapsibleContainer>
        </TitledCutCornerContainer>
    </AnimateInContainer>
    <WaitCover text="Signing in..." :show=showCredWait></WaitCover>
</template>

<style scoped>
* {
    --fwidth: min(calc(100% - 4px), 400px);
    --hwidth: min(calc(50% - 6px), 196px);
}

.nowrap {
    width: 100%;
    text-wrap: nowrap;
    word-wrap: nowrap;
}

.profileTeamSection {
    background-color: #222;
    margin-bottom: 8px;
    padding: 4px 8px;
    border-radius: 8px;
}

.profileTeamGrid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    row-gap: 16px;
    column-gap: 16px;
}

.profileTeamList {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
    row-gap: 8px;
    column-gap: 8px;
}

.profileSaveButton {
    position: absolute;
    bottom: 12px;
    right: 8px;
}

.profileDangerButtons {
    display: grid;
    grid-template-columns: 1fr 1fr;
    column-gap: 12px;
    row-gap: 12px;
    width: 100%;
}

.profileDangerButtons>* {
    width: 100%;
    min-width: 0px;
    margin: 0px 0px;
}
</style>, AccountOpResult, getAccountOpMessage, getTeamOpMessage, TeamOpResult, AccountOpResult, getAccountOpMessage, getTeamOpMessage, TeamOpResult, getAccountOpMessage, getTeamOpMessage, TeamOpResult, TeamOpResult