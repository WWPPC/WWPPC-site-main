<script setup lang="ts">
import GlitchSectionTitle from '#/common-components/GlitchSectionTitle.vue';
import { AnimateInContainer, CenteredContainer, TitledDoubleCutCornerContainer } from '#/containers';
import { InputLinkButton } from '#/inputs';
import { GlitchText } from '#/text';
</script>

<template>
    <div id="home" class="fullBlock stretchBlock">
        <a name="home"></a>
        <GlitchSectionTitle text="WWPIT Archive" font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="spacer"></div>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-column: 1 / -1;">
                <TitledDoubleCutCornerContainer title="Spring 2024" height="100%" align="center" hover-animation="lift" flipped>
                    <CenteredContainer style="font-size: var(--font-20);">
                        <div class="centered" style="margin-top: 0.5em;">
                            <AnimateInContainer type="fade" :delay=400 style="grid-row: 1 / -1;">
                                <RouterLink to="/contest/upsolve" no-deco>
                                    <InputLinkButton text="Upsolve" font-size="var(--font-large)" color="lime"></InputLinkButton>
                                </RouterLink>
                            </AnimateInContainer>
                            <AnimateInContainer type="fade" :delay=400 style="grid-row: 1 / -1;">
                                <RouterLink to="/contestArchive/2024" no-deco>
                                    <InputLinkButton text="Contest Page" font-size="var(--font-large)" color="lime"></InputLinkButton>
                                </RouterLink>
                            </AnimateInContainer>
                        </div>
                    </CenteredContainer>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
        </div>
    </div>
</template>

<style scoped>
.homeColumns {
    display: grid;
    grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
    row-gap: 24px;
    column-gap: 24px;
    flex-grow: 1;
}

.contestArchiveTitle {
    transform-origin: top;
    transform: translate3D(0px, -20vh, -50px) scale(150%);
    z-index: -1;
    text-align: center;
}

.contestInfoBlock {
    display: grid;
    grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
    grid-template-rows: min-content minmax(0, 1fr);
    grid-auto-flow: column dense;
    /* flexbox moment */
    min-height: 0px;
    row-gap: 24px;
    column-gap: 24px;

}

.spacer {
    flex-grow: 0.5;
}

.stretchBlock {
    display: flex;
    flex-direction: column;
}
</style>