<script setup lang="ts">
import { PanelBody, PanelHeader, PanelMain, PanelNavButton, PanelNavList, PanelRightList, PanelView, PanelNavLargeLogo } from '#/panels';
import UserDisp from '#/common-components/UserDisp.vue';
import { useRoute } from 'vue-router';
import { ref, watch } from 'vue';
import { useConnectionEnforcer } from '#/scripts/ConnectionEnforcer';
import PagePanel2024Archive from './archive/PagePanel2024Archive.vue';

const route = useRoute();
const ignoreServer = ref(route.query.ignore_server !== undefined);
watch(() => route.query.ignore_server, () => {
    ignoreServer.value = route.query.ignore_server !== undefined;
});

const connectionEnforcer = useConnectionEnforcer();

connectionEnforcer.connectionExclude.add('/contestArchive');
connectionEnforcer.loginExclude.add('/contestArchive');

</script>

<template>
    <PanelView name="contestArchive" title="WWPIT">
        <PanelHeader>
            <PanelNavLargeLogo></PanelNavLargeLogo>
            <PanelNavList>
                <PanelNavButton text="Home" for="/home"></PanelNavButton>
                <PanelNavButton text="Back" for="/contest/archive"></PanelNavButton>
                <PanelNavButton text="2024" for="/contestArchive/2024"></PanelNavButton>
                <PanelNavButton text="Coming Soon" for=""></PanelNavButton>
            </PanelNavList>
            <PanelRightList>
                <UserDisp></UserDisp>
            </PanelRightList>
        </PanelHeader>
        <PanelMain>
            <PanelBody name="2024" title="2024" scroll-snap>
                <PagePanel2024Archive></PagePanel2024Archive>
            </PanelBody>
        </PanelMain>
    </PanelView>
</template>

<style scoped></style>