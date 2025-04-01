<script setup lang="ts">
import ContactFooter from '#/common/ContactFooter.vue';
import ScrollIndicator from '#/common/ScrollIndicator.vue';
import { AnimateInContainer, CenteredContainer, TitledDoubleCutCornerContainer, CutCornerContainer, TitledCollapsibleContainer, AngledTitledContainer } from '#/containers';
import { InputLinkButton } from '#/inputs';
import { GlitchText } from '#/text';
</script>

<template>
    <div class="fullBlock stretchBlock">
        <GlitchText text="WWPHacks" class="hackathonTitle" font-size="var(--font-title)" color="lime" shadow glow :steps=2 :delay=10 random on-visible></GlitchText>
        <div class="hacksInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-row: span 2;">
                <TitledDoubleCutCornerContainer title="Come hack with us!" height="100%" align="center" hover-animation="lift">
                    <p>
                        Join us for 24 hours of hackathon-ing at Princeton High School
                    </p>
                    <!-- insert image here lol -->
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=200>
                <TitledDoubleCutCornerContainer title="WWP-Princeton Hacks 2024" height="100%" align="center" hover-animation="lift" flipped>
                    <div class="centered">
                        <GlitchText text="12/18/2024" font-size="var(--font-huge)" color="red" glow random flashing :steps=5 start-glitched></GlitchText>
                    </div>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=300>
                <CutCornerContainer height="100%" hover-animation="lift" vertical-flipped>
                    <CenteredContainer>
                        <span style="font-size: var(--font-20);">
                            <br>
                            <div class="centered" style="margin: 4px;">
                                <InputLinkButton text="Register" color="lime" font-size="var(--font-large)" disabled></InputLinkButton>
                            </div>
                            <i style="font-size: var(--font-16)">Registrations are not open yet, check back later!</i>
                        </span>
                    </CenteredContainer>
                </CutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageHackathonScrollTo]"></ScrollIndicator>
    </div>
    <div class="fullBlock">
        <a name="pageHackathonScrollTo"></a>
        <div class="hacksColumns">
            <div class="stretchBlock hacksTilesColumn">
                <AnimateInContainer type="slideUp" show-on-screen>
                    <CutCornerContainer hover-animation="lift">
                        buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh
                    </CutCornerContainer>
                </AnimateInContainer>
                <AnimateInContainer type="slideUp" show-on-screen>
                    <CutCornerContainer hover-animation="lift">
                        buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh
                    </CutCornerContainer>
                </AnimateInContainer>
                <AnimateInContainer type="slideUp" show-on-screen>
                    <CutCornerContainer hover-animation="lift">
                        buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh
                    </CutCornerContainer>
                </AnimateInContainer>
                <AnimateInContainer type="slideUp" show-on-screen>
                    <CutCornerContainer hover-animation="lift">
                        buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh
                    </CutCornerContainer>
                </AnimateInContainer>
                <AnimateInContainer type="slideUp" show-on-screen>
                    <CutCornerContainer hover-animation="lift">
                        buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh
                    </CutCornerContainer>
                </AnimateInContainer>
                <AnimateInContainer type="slideUp" show-on-screen>
                    <CutCornerContainer hover-animation="lift">
                        buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh<br>buh
                    </CutCornerContainer>
                </AnimateInContainer>
            </div>
            <div>
                <div class="hacksStickyBox">
                    <CenteredContainer>
                        <GlitchText text="idk lol" font-size="var(--font-title)" color="lime" glow shadow random :steps=2 on-visible></GlitchText>
                    </CenteredContainer>
                    <AnimateInContainer type="fade" show-on-screen>
                        <AngledTitledContainer title="Title" hover-animation="lift">
                            content content content content content content content content content content content content content content content content content content content content content content content
                        </AngledTitledContainer>
                        <AngledTitledContainer title="Title" hover-animation="lift" flipped>
                            content content content content content content content content content content content content content content content content content content content content content content content
                        </AngledTitledContainer>
                    </AnimateInContainer>
                </div>
            </div>
        </div>
        <ScrollIndicator anchor="a[name=pageHackathonScrollTo2]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageHackathonScrollTo2"></a>
        <CenteredContainer>
            <GlitchText text="idk" font-size="var(--font-title)" color="lime" glow shadow random :steps=2 on-visible></GlitchText>
        </CenteredContainer>
        <ScrollIndicator anchor="a[name=pageHackathonScrollTo3]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageHackathonScrollTo3"></a>
        <CenteredContainer>
            <GlitchText text="FAQ" font-size="var(--font-title)" color="lime" glow shadow random :steps=2 :delay=10 on-visible></GlitchText>
        </CenteredContainer>
        <div class="faq">
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="When is it?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        <i>All information is tentative as of now.</i>
                        <br>
                        WWPHacks is expected to happen towards of the start of the 2024-2025 school year.
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="Where will it be held?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        <i>All information is tentative as of now.</i>
                        <br>
                        We can't say anything about possible venues yet.
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="How many people can be on a team?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        <i>All information is tentative as of now.</i>
                        <br>
                        Expect to have teams of 3-4 people
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
        </div>
        <div class="spacer"></div>
        <ContactFooter></ContactFooter>
    </div>
</template>

<style scoped>
.hackathonTitle {
    transform-origin: top;
    transform: translate3D(0px, -20vh, -50px) scale(150%);
    z-index: -1;
    text-align: center;
}

.hacksInfoBlock {
    display: grid;
    grid-template-columns: minmax(0, 1fr) minmax(0, 1fr);
    grid-template-rows: min-content minmax(0, 1fr);
    grid-auto-flow: column dense;
    /* flexbox moment */
    min-height: 0px;
    row-gap: 24px;
    column-gap: 24px;
    flex: 1;
}

.hacksInfoBlock>div {
    height: 100%;
}

.hacksColumns {
    display: flex;
    flex-direction: row;
    column-gap: 24px;
}

.hacksColumns>div {
    flex-grow: 1;
    width: 100%;
}

.hacksTilesColumn {
    row-gap: 24px;
}

.hacksStickyBox {
    position: sticky;
    top: 0px;
    bottom: 0px;
}

@media (max-width: 100vh) {
    .hacksInfoBlock {
        grid-template-columns: minmax(0, 1fr);
        grid-template-rows: repeat(4, min-content);
        grid-auto-flow: column;
        min-height: min-content;
    }

    .hacksInfoBlock>div:nth-child(2) {
        order: -1;
    }
}

.faq {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(400px, 100%), 1fr));
    width: 100%;
    row-gap: 24px;
    column-gap: 24px;
}

.spacer {
    flex-grow: 1;
}

.faq>div {
    max-width: 100%;
}
</style>