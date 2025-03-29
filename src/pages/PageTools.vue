<script setup lang="ts">
import { PanelBody, PanelHeader, PanelMain, PanelNavButton, PanelNavList, PanelView, PanelNavLargeLogo } from '#/panels';
import PagePanelToolsEditor from './tools/PagePanelToolsEditor.vue';
import PagePanelToolsDataurl from './tools/PagePanelToolsDataurl.vue';
import PagePanelToolsSvgConverter from './tools/PagePanelToolsSvgConverter.vue';
import PagePanelToolsImageFilter from './tools/PagePanelToolsImageFilter.vue';

</script>

<template>
    <PanelView name="tools" title="WWPPC Tools">
        <PanelHeader>
            <PanelNavLargeLogo></PanelNavLargeLogo>
            <PanelNavList>
                <PanelNavButton text="Tools" for="/tools/index" is-default></PanelNavButton>
                <PanelNavButton text="Problem Editor" for="/tools/editor"></PanelNavButton>
                <PanelNavButton text="Image to Dataurl" for="/tools/dataurl"></PanelNavButton>
                <PanelNavButton text="SVG to PNG" for="/tools/svgconverter"></PanelNavButton>
                <PanelNavButton text="Image Filter" for="/tools/imagefilter"></PanelNavButton>
            </PanelNavList>
        </PanelHeader>
        <PanelMain>
            <PanelBody name="index" is-default>
                <h1>WWPPC Tools</h1>
                <p>You've found the "secret" WWPPC tools!</p>
                <ul>
                    <li><RouterLink to="/tools/editor">Problem Editor</RouterLink></li>
                    <li><RouterLink to="/tools/dataurl">Image to dataurl</RouterLink></li>
                    <li><RouterLink to="/tools/svgconverter">SVG to PNG</RouterLink></li>
                    <li><RouterLink to="/tools/imagefilter">Image Filter</RouterLink></li>
                </ul>
            </PanelBody>
            <PanelBody name="editor" title="Problem Editor">
                <PagePanelToolsEditor></PagePanelToolsEditor>
            </PanelBody>
            <PanelBody name="dataurl" title="Image to Dataurl">
                <PagePanelToolsDataurl></PagePanelToolsDataurl>
            </PanelBody>
            <PanelBody name="svgconverter" title="SVG to PNG">
                <PagePanelToolsSvgConverter></PagePanelToolsSvgConverter>
            </PanelBody>
            <PanelBody name="imagefilter" title="Image Filter">
                <PagePanelToolsImageFilter></PagePanelToolsImageFilter>
            </PanelBody>
        </PanelMain>
    </PanelView>
</template>

<style scoped>
li {
    text-decoration: underline;
    color: lime;
    font-size: var(--font-medium);
    cursor: pointer;
}
</style>