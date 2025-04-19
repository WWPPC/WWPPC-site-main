<script setup lang="ts">
import { FullscreenModal, globalModal } from '#/modal';
import NotFound from '#/common/NotFound.vue';
import PageHome from '@/pages/PageHome.vue';
import PageHackathon from '@/pages/PageWWPHacks.vue';
import PageContest from '@/pages/PageWWPIT.vue';
import PageContestArchive from './pages/PageContestArchive.vue';
import PageAccount from '../WWPPC-site-common/src/common-pages/PageAccount.vue';
import PageUserView from '#/common-pages/PageUserView.vue';
import PageLogin from '#/common-pages/PageLogin.vue';
import PageRecovery from '../WWPPC-site-common/src/common-pages/PageRecovery.vue';
import PageTest from '@/pages/PageTest.vue';
import PageTools from './pages/PageTools.vue';
import SuperSecretFeature from '@/components/SuperSecretFeature.vue';
import SuperSecretCarrier from '@/components/SuperSecretCarrier.vue';
import { ref, watch } from 'vue';
import { useLoginEnforcer } from '#/modules/LoginEnforcer';
import { useServerState } from '#/modules/ServerState';
import { useAccountManager } from '#/modules/AccountManager';
import { useContestManager } from '#/modules/ContestManager';

const serverState = useServerState();
const loginEnforcer = useLoginEnforcer();
const accountManager = useAccountManager();
const contestManager = useContestManager();
loginEnforcer.init();
serverState.init();
accountManager.init();
contestManager.init();

const modalComponent = ref<InstanceType<typeof FullscreenModal>>();
const modal = globalModal();
watch(() => modalComponent.value, () => {
    if (modalComponent.value != undefined) modal.setModal(modalComponent.value);
});

window.addEventListener('error', (err) => {
    modal.showModal({ title: 'An Error Occured', content: `<span style="color: red;">${err.message}<br>${err.filename} ${err.lineno}:${err.colno}</span>`, color: 'red' });
});
</script>

<template name="app">
    <NotFound></NotFound>
    <PageHome></PageHome>
    <PageHackathon></PageHackathon>
    <PageContest></PageContest>
    <PageContestArchive></PageContestArchive>
    <PageAccount></PageAccount>
    <PageUserView></PageUserView>
    <PageLogin></PageLogin>
    <PageRecovery></PageRecovery>
    <PageTest></PageTest>
    <PageTools></PageTools>
    <FullscreenModal ref="modalComponent"></FullscreenModal>
    <SuperSecretFeature></SuperSecretFeature>
    <SuperSecretCarrier></SuperSecretCarrier>
</template>