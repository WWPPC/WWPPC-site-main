<script setup lang="ts">
import { isDev } from '#/index';
import { PanelBody, PanelHeader, PanelMain, PanelNavButton, PanelNavList, PanelRightList, PanelView, PanelNavLargeLogo } from '#/panels';
import UserDisp from '#/common-components/UserDisp.vue';
import PagePanelHomeAbout from '@/pages/home/PagePanelHomeAbout.vue';
import PagePanelHomeHome from '@/pages/home/PagePanelHomeHome.vue';
</script>

<template>
    <PanelView name="home" title="WWPPC" is-default>
        <PanelHeader>
            <PanelNavLargeLogo></PanelNavLargeLogo>
            <PanelNavList>
                <PanelNavButton text="Home" for="/home" is-default></PanelNavButton>
                <PanelNavButton text="WWPPC Math" :for="isDev ? 'http://localhost:5174' : 'https://math.wwppc.tech'" link></PanelNavButton>
                <PanelNavButton text="WWPHacks" for="/hackathon"></PanelNavButton>
                <PanelNavButton text="WWPIT" for="/contest"></PanelNavButton>
                <PanelNavButton text="About Us" for="/home/about"></PanelNavButton>
            </PanelNavList>
            <PanelRightList>
                <UserDisp></UserDisp>
            </PanelRightList>
        </PanelHeader>
        <PanelMain>
            <PanelBody name="home" title="Home" is-default scroll-snap>
                <PagePanelHomeHome></PagePanelHomeHome>
            </PanelBody>
            <PanelBody name="about" title="About">
                <PagePanelHomeAbout></PagePanelHomeAbout>
            </PanelBody>
        </PanelMain>
    </PanelView>
</template>

<style scoped></style>