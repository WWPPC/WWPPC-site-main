<script setup lang="ts">
import { PanelBody, PanelHeader, PanelMain, PanelNavButton, PanelNavList, PanelRightList, PanelView, PanelNavLargeLogo } from '#/panels';
import UserDisp from '#/common-components/UserDisp.vue';
import SuperSecretFeature from '@/components/SuperSecretFeature.vue';
import ContestTimer from '#/common-components/contest/ContestTimer.vue';
import { isMobile, isWebkit } from '#/util/userAgent';
import { AccordionCollapsibleContainer } from '#/accordion';
import { TitledCollapsibleContainer } from '#/containers';
</script>

<template>
    <PanelView name="test" title="Test Page">
        <!-- <div style="width: 100vw; height: 100vh; background-color: black;">
            <div class="centered">
                <GlowText text="503" color="white" font-size="50vh" glow shadow style="font-family: 'Apex Mk3'; line-height: 1em;"></GlowText>
            </div>
            <div class="centered">
                <GlowText text="SERVICE UNAVAILABLE" color="rgb(200, 100, 255)" font-size="18vh" glow shadow style="font-family: 'Apex Mk3'; line-height: 1em;"></GlowText>
            </div>
            <div class="centered">
                <GlowText text="SP^2" color="#3C70FF" font-size="20vh" glow shadow style="font-family: 'Apex Mk3'; line-height: 1em;"></GlowText>
            </div>
        </div> -->
        <PanelHeader>
            <PanelNavLargeLogo></PanelNavLargeLogo>
            <PanelNavList>
                <PanelNavButton text="Home" for="/home"></PanelNavButton>
                <PanelNavButton text="Not Fonts" for="/test/test"></PanelNavButton>
                <PanelNavButton text="Fonts" for="/test/fonts"></PanelNavButton>
            </PanelNavList>
            <PanelRightList>
                <UserDisp></UserDisp>
                <ContestTimer contest="WWPIT"></ContestTimer>
            </PanelRightList>
        </PanelHeader>
        <PanelMain>
            <PanelBody name="test" title="" is-default>
                Is mobile platform: {{ isMobile }}
                <br>
                Is Webkit browser: {{ isWebkit }}
                <AccordionCollapsibleContainer exclusive>
                    <TitledCollapsibleContainer title="buh">
                        oofofoofofofo<br>sdafasdf
                    </TitledCollapsibleContainer>
                    <TitledCollapsibleContainer title="buh">
                        oofofoofofofo<br><br>adskj
                    </TitledCollapsibleContainer>
                    <TitledCollapsibleContainer title="buh">
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                        oofofoofofofo<br>buhaAAAAAAAAAAAAAAAAAAAAAc
                    </TitledCollapsibleContainer>
                    <TitledCollapsibleContainer title="buh">
                        oofofoofofofo<br><br><br><br><br>>>>>>>>>boh
                    </TitledCollapsibleContainer>
                </AccordionCollapsibleContainer>
            </PanelBody>
            <PanelBody name="fonts" title="Fonts">
                <span style="font-size: var(--font-huge-title);">Huge Title</span>
                <br>
                <span style="font-size: var(--font-title);">Title</span>
                <br>
                <span style="font-size: var(--font-subtitle);">Subtitle</span>
                <br>
                <span style="font-size: var(--font-subsubtitle);">Sub-Subtitle</span>
                <br>
                <h1>Header 1</h1>
                <h2>Header 2</h2>
                <h3>Header 3</h3>
                <p>Paragraph</p>
                <p><b>Bold</b></p>
                <p><i>Italic</i></p>
                <code>const buh: number = NaN;</code>
                <codeblock>function add(...nums) {
return nums.reduce((p, c) => p + c, 0);
}</codeblock>
                <p style="font-size: var(--font-16);">Size 16</p>
                <p style="font-size: var(--font-18);">Size 18</p>
                <p style="font-size: var(--font-20);">Size 20</p>
                <p style="font-size: var(--font-24);">Size 24</p>
                <p style="font-size: var(--font-28);">Size 28</p>
                <p style="font-size: var(--font-32);">Size 32</p>
                <p style="font-size: var(--font-40);">Size 40</p>
                <p style="font-size: var(--font-48);">Size 48</p>
                <p style="font-size: var(--font-small);">Small</p>
                <p style="font-size: var(--font-medium);">Medium</p>
                <p style="font-size: var(--font-large);">Large</p>
                <p style="font-size: var(--font-huge);">Huge</p>
            </PanelBody>
        </PanelMain>
        <SuperSecretFeature show></SuperSecretFeature>
    </PanelView>
</template>

<style scoped></style>