<script setup lang="ts">
import ScrollIndicator from '#/common/ScrollIndicator.vue';
import { AnimateInContainer, CenteredContainer, DoubleCutCornerContainer } from '#/containers';
import { GlowText, GlitchText } from '#/text';
import { InputLinkButton, InputIconButton } from '#/inputs';
import LineDivider from '#/common/LineDivider.vue';
import ContactFooter from '#/common/ContactFooter.vue';
import { nextContest, nextContestEnd } from '@/scripts/contestInfo';
import GlitchSectionTitle from '#/common-components/GlitchSectionTitle.vue';
</script>

<template>
    <div class="fullBlock stretchBlock">
        <GlitchSectionTitle text="WWPPC 2025" parallax font-size="var(--font-huge-title)"></GlitchSectionTitle>
        <div class="homeColumns">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100>
                <DoubleCutCornerContainer height="100%" hover-animation="lift">
                    <CenteredContainer height="100%">
                        <div class="homeVertical">
                            <div style="flex-grow: 1;">
                                <GlitchText text="WWPHacks" font-size="var(--font-subtitle)" color="lime" glow shadow :steps=3 :delay=10 random></GlitchText>
                                <GlitchText text="??/??/????" font-size="var(--font-subsubtitle)" color="red" glow :steps=1 :delay=Infinity start-glitched></GlitchText>
                                <LineDivider color="#AAA"></LineDivider>
                                <p>
                                    WWPHacks is a hackathon - a collaborative programming competition where teams work against the clock to build innovative solutions to real-world problems.
                                </p>
                            </div>
                            <div style="display: flex; flex-direction: column;">
                                <GlowText text="" font-size="var(--font-28)" color="lime" glow flashing></GlowText>
                                <div class="centered" style="margin-top: 0.5em;">
                                    <AnimateInContainer type="fade" :delay=400>
                                        <RouterLink to="/hackathon" no-deco>
                                            <InputLinkButton text="Contest Page" font-size="var(--font-large)" color="lime"></InputLinkButton>
                                        </RouterLink>
                                    </AnimateInContainer>
                                </div>
                            </div>
                        </div>
                    </CenteredContainer>
                </DoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=200>
                <DoubleCutCornerContainer height="100%" hover-animation="lift">
                    <CenteredContainer height="100%">
                        <div class="homeVertical">
                            <div style="flex-grow: 1;">
                                <GlitchText text="WWPIT" font-size="var(--font-subtitle)" color="lime" glow shadow :steps=3 :delay=10 random></GlitchText>
                                <GlitchText :text="`${String(nextContest.getMonth() + 1).padStart(2, '0')}/${String(nextContest.getDate()).padStart(2, '0')}/${nextContest.getFullYear()}`" font-size="var(--font-subsubtitle)" color="red" glow random flashing :delay=10 start-glitched></GlitchText>
                                <LineDivider color="#AAA"></LineDivider>
                                <p>
                                    WWPIT is a round-based informatics tournament with multiple divisions for competitive programmers of all skill levels.
                                </p>
                            </div>
                            <div style="display: flex; flex-direction: column;">
                                <GlitchText text="Registrations open!" font-size="var(--font-28)" color="lime" glow flashing random v-if="Date.now() < nextContest.getTime()"></GlitchText>
                                <GlitchText text="Contest ended!" font-size="var(--font-28)" color="red" glow random v-else-if="Date.now() > nextContestEnd.getTime()"></GlitchText>
                                <GlitchText text="Contest started!" font-size="var(--font-28)" color="lime" glow flashing flash-color="red" random v-else></GlitchText>
                                <div class="centered" style="margin-top: 0.5em;">
                                    <AnimateInContainer type="fade" :delay=400>
                                        <RouterLink to="/contest" no-deco>
                                            <InputLinkButton text="Contest Page" font-size="var(--font-large)" color="lime"></InputLinkButton>
                                        </RouterLink>
                                    </AnimateInContainer>
                                </div>
                            </div>
                        </div>
                    </CenteredContainer>
                </DoubleCutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageHomeScrollTo]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageHomeScrollTo"></a>
        <div class="centered">
            <GlitchSectionTitle text="About WWPPC" font-size="var(--font-title)"></GlitchSectionTitle>
        </div>
        <div class="homeGeneralInfoColumns" style="font-size: var(--font-medium);">
            <AnimateInContainer type="slideUp" show-on-screen style="grid-row: span 2;">
                <DoubleCutCornerContainer height="100%" hover-animation="lift">
                    <div class="centered" style="height: 4em;">
                        <img src="/icon2-small.png">
                    </div>
                    <p style="text-wrap: balanced; margin: 0px 8px;">
                        WWPPC is the host of competitions like WWPIT and WWPHacks, run by students at WW-P High School South.
                    </p>
                    <p style="text-wrap: balanced; color: lime; margin: 0px 8px;">
                        WWPPC is a 501c3 nonprofit organization.
                    </p>
                </DoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <DoubleCutCornerContainer height="100%" hover-animation="lift">
                    <p style="text-wrap: balanced;">
                        Check out our math division for <span style="color: lime;">math & informatics tournaments</span>!
                    </p>
                    <div style="text-align: center">
                        <a href="https://math.wwppc.tech" target="_blank" class="centered" style="text-decoration: none;">
                            <InputIconButton text="WWPPC Math" img="/icon2-small.png" color="lime" font-size="var(--font-28)" no-mask></InputIconButton>
                        </a>
                    </div>
                </DoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen style="grid-row: span 2;">
                <DoubleCutCornerContainer height="100%" hover-animation="lift">
                    <p style="text-wrap: balance; font-size: var(--font-20); margin-top: 0px;">
                        <span style="color: lime;">WWPPC</span>:
                        West Windsor Plainsboro Programming Competitions
                    </p>
                    <p style="text-wrap: balance; font-size: var(--font-20); margin-top: 0px;">
                        <span style="color: lime;">WWPIT</span>:
                        West Windsor Plainsboro Informatics Tournament
                    </p>
                    <p style="text-wrap: balance; font-size: var(--font-20); margin: 0px 8px;">
                        <span style="color: lime;">WWPHacks</span>:
                        WWPHacks <i>(not an acronym)</i>
                    </p>
                    <LineDivider margin="0px"></LineDivider>
                    <p style="text-wrap: balance; font-size: var(--font-16);">
                        <i>WWPPC is not affiliated with or endorsed by the West Windsor-Plainsboro Regional School District</i>
                    </p>
                </DoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <DoubleCutCornerContainer height="100%" hover-animation="lift">
                    <a href="https://discord.wwppc.tech" target="_blank" class="centered" no-deco>
                        <InputIconButton text="Join us on Discord!" img="/img/discord-logo.svg" color="lime" font-size="var(--font-medium)" img-hover-color="#5865F2"></InputIconButton>
                    </a>
                    <div style="height: 0.5em;"></div>
                    <a href="https://github.com/WWPPC" target="_blank" class="centered" no-deco>
                        <InputIconButton text="GitHub" img="/img/github-logo.svg" color="lime" font-size="var(--font-medium)" img-hover-color="#F05032"></InputIconButton>
                    </a>
                </DoubleCutCornerContainer>
            </AnimateInContainer>
        </div>
        <ContactFooter></ContactFooter>
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

@media (max-width: 100vh) {
    .homeColumns {
        grid-template-columns: 1fr;
        grid-template-rows: min-content min-content;
    }
}

.homeVertical {
    display: flex;
    height: 100%;
    flex-direction: column;
    justify-items: stretch;
}

p {
    text-align: center;
}

.homeGeneralInfoColumns {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(400px, 100%), 1fr));
    flex-grow: 1;
    justify-items: stretch;
    row-gap: 24px;
    column-gap: 24px;
}

.spacer {
    flex-grow: 1;
}
</style>