<script setup lang="ts">
import { PanelBody, PanelHeader, PanelMain, PanelNavButton, PanelNavList, PanelRightList, PanelView, PanelNavLargeLogo } from '#/panels';
import UserDisp from '#/common-components/UserDisp.vue';
import ContestTimer from '#/common-components/contest/ContestTimer.vue';
import { useRoute } from 'vue-router';
import PagePanelContestInfo from './contest/PagePanelContestInfo.vue';
import PagePanelContestContest from '#/common-pages/contest/PagePanelContestContest.vue';
import PagePanelContestProblemList from '#/common-pages/contest/PagePanelContestProblemList.vue';
import PagePanelContestProblemView from '#/common-pages/contest/PagePanelContestProblemView.vue';
import PagePanelContestLeaderboard from '#/common-pages/contest/PagePanelContestLeaderboard.vue';
import PagePanelArchiveList from './archive/PagePanelArchiveList.vue';
import { ref, watch } from 'vue';
import { useContestManager } from '#/modules/ContestManager';
import { useLoginEnforcer } from '#/modules/LoginEnforcer';

const route = useRoute();
const ignoreServer = ref(route.query.ignore_server !== undefined);
watch(() => route.query.ignore_server, () => {
    ignoreServer.value = route.query.ignore_server !== undefined;
});

const loginEnforcer = useLoginEnforcer();
const contestManager = useContestManager();

loginEnforcer.connectionInclude.add('/contest');
loginEnforcer.loginInclude.add('/contest');
loginEnforcer.connectionExcludeExact.add('/contest/home');
loginEnforcer.loginExcludeExact.add('/contest/home');
loginEnforcer.connectionExcludeExact.add('/contest');
loginEnforcer.loginExcludeExact.add('/contest');
loginEnforcer.loginExclude.add('/contest/archive');
</script>

<template>
    <PanelView name="contest" title="WWPIT">
        <PanelHeader>
            <PanelNavLargeLogo></PanelNavLargeLogo>
            <PanelNavList>
                <PanelNavButton text="Home" for="/home"></PanelNavButton>
                <PanelNavButton text="WWPIT" for="/contest/home" is-default></PanelNavButton>
                <PanelNavButton text="Archive" for="/contest/archive"></PanelNavButton>
                <div v-if="contestManager.contests.WWPIT != null || ignoreServer" style="display: flex;">
                    <PanelNavButton text="Contest" for="/contest/contest"></PanelNavButton>
                    <PanelNavButton text="Problems" for="/contest/problemList"></PanelNavButton>
                    <PanelNavButton text="Leaderboard" for="/contest/leaderboard"></PanelNavButton>
                </div>
            </PanelNavList>
            <PanelRightList>
                <UserDisp></UserDisp>
                <ContestTimer contest="WWPIT"></ContestTimer>
            </PanelRightList>
        </PanelHeader>
        <PanelMain>
            <PanelBody name="home" title="Home" is-default scroll-snap>
                <PagePanelContestInfo></PagePanelContestInfo>
            </PanelBody>
            <PanelBody name="contest" title="Contest" scroll-snap>
                <PagePanelContestContest contest="WWPIT"></PagePanelContestContest>
            </PanelBody>
            <PanelBody name="problemList" title="Problem List">
                <PagePanelContestProblemList contest="WWPIT"></PagePanelContestProblemList>
            </PanelBody>
            <PanelBody name="problemView" title="Problem">
                <PagePanelContestProblemView contest="WWPIT"></PagePanelContestProblemView>
            </PanelBody>
            <PanelBody name="leaderboard" title="Leaderboard">
                <PagePanelContestLeaderboard contest="WWPIT"></PagePanelContestLeaderboard>
            </PanelBody>
            <PanelBody name="archive" title="Archive">
                <PagePanelArchiveList></PagePanelArchiveList>
            </PanelBody>
            <PanelBody name="archiveView" title="Archive Problem">
                <PagePanelContestProblemView  contest="WWPIT" isUpsolve></PagePanelContestProblemView>
            </PanelBody>
        </PanelMain>
    </PanelView>
</template>

<style scoped></style>