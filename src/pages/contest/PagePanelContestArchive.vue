<script setup lang="ts">
import { MultipaneSelectorContainer, MultipaneSelector, MultipanePaneContainer, MultipanePane } from '#/multipane';
import { AnimateInContainer, CenteredContainer, TitledDoubleCutCornerContainer, DoubleCutCornerContainer, CutCornerContainer, TitledCollapsible, HeaderedTable } from '#/containers';
import LineDivider from '#/common/LineDivider.vue';
import ContactFooter from '#/common/ContactFooter.vue';
import ScrollIndicator from '#/common/ScrollIndicator.vue';
import { InputLinkButton, InputIconButton } from '#/inputs';
import { globalModal, FullscreenModal} from '#/modal';
import { GlitchText, GlowText } from '#/text';
import TimerDisplay from '#/common/TimerDisplay.vue';
import HomeSponsorLogo from '#/common-components/home/home/HomeSponsorLogo.vue';
import { nextContest, nextContestEnd } from '@/scripts/contestInfo';
import PagePanelContestInfo from './PagePanelContestInfo.vue';

// const modal = new FullscreenModal();

// const showS2024 = async () => {
//     modal.showModal({title: 'Spring 2024', content: 'skibidi'});
//     modal.showModal({title: 'Spring2024', content: 'skibidi'});
// }

function scrollToElement(elementId: string) {
    const element = document.getElementById(elementId);
    element?.scrollIntoView({behavior: "smooth"});
}

</script>

<template>
    <div id="home" class="fullBlock stretchBlock">
        <a name="home"></a>
        <GlitchText text="Contest Archive" class="previousContestTitle" font-size="var(--font-title)" color="lime" shadow glow :steps=2 :delay=10 random on-visible></GlitchText>
        <div class="spacer"></div>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-column: 1 / -1;">
                <TitledDoubleCutCornerContainer title="Spring 2024" height="100%" align="center" hover-animation="lift" flipped>
                    <CenteredContainer style="font-size: var(--font-20);">
                        <div class="centered" style="margin-top: 0.5em;">
                            <AnimateInContainer type="fade" :delay=400 style="grid-row: 1 / -1;">
                                <InputLinkButton text="Upsolve" font-size="var(--font-large)" color="lime"></InputLinkButton> 
                            </AnimateInContainer>
                            <AnimateInContainer type="fade" :delay=400 style="grid-row: 1 / -1;">
                                <InputLinkButton text="Winners" font-size="var(--font-large)" color="lime" v-on:click="scrollToElement('spring2024')"></InputLinkButton>
                            </AnimateInContainer>
                        </div>
                    </CenteredContainer>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-column: 1 / -1;">
                <TitledDoubleCutCornerContainer title="Coming Soon" height="100%" align="center" hover-animation="lift" flipped>
                    <CenteredContainer style="font-size: var(--font-20);">
                        <div class="centered" style="margin-top: 0.5em;">
                            <AnimateInContainer type="fade" :delay=400 style="grid-row: 1 / -1;">
                                <InputLinkButton text="Upsolve" font-size="var(--font-large)" color="lime"></InputLinkButton> 
                            </AnimateInContainer>
                            <AnimateInContainer type="fade" :delay=400 style="grid-row: 1 / -1;">
                                <InputLinkButton text="Winners" font-size="var(--font-large)" color="lime"></InputLinkButton>
                            </AnimateInContainer>
                        </div>
                    </CenteredContainer>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
        
        </div>
    </div>
    <div id="spring2024" class="fullBlock stretchBlock">
        <a name="spring2024"></a>
        <CenteredContainer>
            <GlitchText text="Spring 2024" font-size="var(--font-title)" color="lime" shadow glow :steps=2 :delay=10 random on-visible></GlitchText>
        </CenteredContainer>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-row: span 2;">
                <AnimateInContainer type="slideUp" show-on-screen :delay=200>
                    <TitledDoubleCutCornerContainer title="Novice" height="100%" align="center" hover-animation="lift" flipped>
                        <div class="centered">
                            <div class="contestWinnerTable">
                                <span>🥇</span>
                                <div class="contestWinnerBlock">
                                    <span>PHS CPT Amogus:</span>
                                    <span>
                                        (
                                        <RouterLink to="/user/@ommehta16">Om Mehta</RouterLink>,
                                        <RouterLink to="/user/@square-brackets">Allan Chen</RouterLink>,
                                        <RouterLink to="/user/@imkindabad">Oscar Huang</RouterLink>,
                                        <RouterLink to="/user/@jonathanji">Jonathan Ji</RouterLink>
                                        )
                                    </span>
                                </div>
                                <span>🥈</span>
                                <div class="contestWinnerBlock">
                                    <span>BinaryThree</span>
                                    <span>
                                        (
                                        <RouterLink to="/user/@litvinas">Fiodar Ziuzin</RouterLink>,
                                        <RouterLink to="/user/@trgt26">Junayed Ahammed</RouterLink>
                                        )
                                    </span>
                                </div>
                                <span>🥉</span>
                                <div class="contestWinnerBlock">
                                    <span>PuppyImpression</span>
                                    <span>
                                        (
                                        <RouterLink to="/user/@natnuo">Nathan Tao</RouterLink>,
                                        <RouterLink to="/user/@adabot">Ada Langford</RouterLink>
                                        )
                                    </span>
                                </div>
                            </div>
                        </div>
                    </TitledDoubleCutCornerContainer>
                </AnimateInContainer>
                <ScrollIndicator anchor="a[name=spring2024]" ></ScrollIndicator>
                <AnimateInContainer type="slideUp" show-on-screen :delay=100>
                    <TitledDoubleCutCornerContainer title="Advanced" height="100%" align="center" hover-animation="lift" >
                        <div class="centered">
                            <div class="contestWinnerTable">
                                <span>🥇</span>
                                <div class="contestWinnerBlock">
                                    <span>liympanda</span>
                                    <span>
                                        (
                                        <RouterLink to="/user/@liympanda">Yiming Li</RouterLink>
                                        )
                                    </span>
                                </div>
                                <span>🥈</span>
                                <div class="contestWinnerBlock">
                                    <span>oursaco</span>
                                    <span>
                                        (
                                        <RouterLink to="/user/@oursaco">Thomas Liu</RouterLink>
                                        )
                                    </span>
                                </div>
                                <span>🥉</span>
                                <div class="contestWinnerBlock">
                                    <span>tfg</span>
                                    <span>
                                        (
                                        <RouterLink to="/user/@tristansun">Tristan Sun</RouterLink>,
                                        <RouterLink to="/user/@axujls">Andrew Xu</RouterLink>,
                                        <RouterLink to="/user/@colecancode">Cole Miller</RouterLink>,
                                        <RouterLink to="/user/@pikachu2021">Soham Samanta</RouterLink>
                                        )
                                    </span>
                                </div>
                            </div>
                        </div>
                    </TitledDoubleCutCornerContainer>
                </AnimateInContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=200 style="grid-column: 1;">
                <DoubleCutCornerContainer title="Date" height="100%" width="100%" align="center" hover-animation="lift">
                    <div class="centered">
                        <GlitchText text="<<< 06/02/2024 >>>" font-size="var(--font-large)" color="red" glow random flashing :steps=5 start-glitched></GlitchText>
                    </div>
                    <div class="centered" v-if="Date.now() < nextContest.getTime()">
                        <TimerDisplay :to="nextContest" type="clock" font-size="var(--font-large)" color="lime" glow></TimerDisplay>
                    </div>
                </DoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=300>
                <AnimateInContainer type="slideUp" show-on-screen :delay=300>
                    <TitledDoubleCutCornerContainer title="Sponsors" height="100%" width="100%" align="center" hover-animation="lift">
                        <div class="sponsorColumns">
                            <div>
                                <GlowText text="PARTNERS" font-size="var(--font-medium)" color="lime" shadow></GlowText>
                                <HomeSponsorLogo src="/img/cpi-logo.svg" url="https://joincpi.org/" name="CPI Logo" height="6vh"></HomeSponsorLogo>
                            </div>
                            <div>
                                <GlowText text="GOLD" font-size="var(--font-medium)" color="#FD0" shadow></GlowText>
                                <HomeSponsorLogo src="/img/x-camp-logo.png" url="https://x-camp.academy/" name="X-Camp Logo" height="5vh"></HomeSponsorLogo>
                            </div>
                            <div>
                                <GlowText text="SILVER" font-size="var(--font-medium)" color="#CCC" shadow></GlowText>
                                <HomeSponsorLogo src="/img/icode-logo.png" url="https://icodeschool.com/" name="ICode Logo" height="5vh"></HomeSponsorLogo>
                            </div>
                        </div>
                        <LineDivider color="#AAA"></LineDivider>
                        <div class="sponsors">
                            <HomeSponsorLogo src="/img/desmos-logo.svg" url="https://desmos.com/" name="Desmos Logo" height="1.375vh"></HomeSponsorLogo>
                            <HomeSponsorLogo src="/img/aops-logo.svg" url="https://artofproblemsolving.com/" name="AoPS Logo" height="3vh"></HomeSponsorLogo>
                            <HomeSponsorLogo src="/img/xyz-logo.svg" url="https://gen.xyz" name=".xyz Logo" height="2.25vh"></HomeSponsorLogo>
                            <HomeSponsorLogo src="/img/echo3d-logo.png" url="https://www.echo3d.com/" name="Echo3D Logo" height="1.375vh"></HomeSponsorLogo>
                            <HomeSponsorLogo src="/img/axure-logo.svg" url="https://axure.com/" name="Axure Logo" height="1.5vh"></HomeSponsorLogo>
                        </div>
                    </TitledDoubleCutCornerContainer>
                </AnimateInContainer>
                <AnimateInContainer type="slideUp" show-on-screen :delay=300>
                    <DoubleCutCornerContainer border-color="black" height="100%" width="100%" align="center" hover-animation="lift">
                    </DoubleCutCornerContainer>
                </AnimateInContainer>
                <AnimateInContainer type="slideUp" show-on-screen :delay=300>
                    <TitledDoubleCutCornerContainer title="Organizers" height="100%" width="100%" align="center" hover-animation="lift">
                    
                    </TitledDoubleCutCornerContainer>
                </AnimateInContainer>
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

.previousContestTitle {
    transform-origin: top;
    transform: translate3D(0px, -20vh, -50px) scale(150%);
    z-index: -1;
    text-align: center;
}

.stretchBlock {
    display: flex;
    flex-direction: column;
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

.contestInfoBlock>div {
    height: 100%;
}

.scheduleBlock {
    display: grid;
    grid-template-columns: min-content 1fr;
    row-gap: 16px;
    column-gap: 16px;
    flex-grow: 1;
}

@media (max-width: 100vh) {
    .contestInfoBlock {
        grid-template-columns: minmax(0, 1fr);
        grid-template-rows: repeat(4, min-content);
        grid-auto-flow: column;
        min-height: min-content;
    }

    .scheduleBlock {
        grid-template-columns: minmax(0, 1fr);
        grid-template-rows: min-content min-content;
    }
}

.contestWinnerTable {
    display: grid;
    grid-template-columns: 2em 1fr;
    font-size: var(--font-32);
}

.contestWinnerTable>span:nth-child(even) {
    color: lime;
    text-decoration: underline;
    cursor: pointer;
}

.contestWinnerBlock {
    display: flex;
    flex-direction: column;
    font-size: var(--font-20);
}

.contestWinnerBlock>span:nth-child(2) {
    font-size: var(--font-16);
}

.winnersBlock {
    grid-auto-flow: row dense;
    grid-template-rows: minmax(0, 1fr) min-content;
}

.winnersBlock>div:nth-child(3) {
    grid-column: span 2;
}

@media (max-width: 100vh) {
    .winnersBlock>div:nth-child(3) {
        grid-column: 1;
    }
}

.spacer {
    flex-grow: 0.5;
}

.sponsorColumns {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: space-around;
    padding: 0px 5%;
}

.sponsorColumns>div {
    width: 40vh;
    display: flex;
    flex-direction: column;
    align-items: center;
}

.sponsors {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    row-gap: 25px;
    column-gap: 50px;
    padding: 0px 5%;
}
</style>