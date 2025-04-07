<script setup lang="ts">
import { MultipaneSelectorContainer, MultipaneSelector, MultipanePaneContainer, MultipanePane } from '#/multipane';
import { AnimateInContainer, CenteredContainer, TitledDoubleCutCornerContainer, CutCornerContainer, TitledCollapsible, HeaderedTable } from '#/containers';
import LineDivider from '#/common/LineDivider.vue';
import ContactFooter from '#/common/ContactFooter.vue';
import ScrollIndicator from '#/common/ScrollIndicator.vue';
import { InputLinkButton, InputIconButton } from '#/inputs';
import { GlitchText, GlowText } from '#/text';
import TimerDisplay from '#/common/TimerDisplay.vue';
import HomeSponsorLogo from '#/common-components/home/home/HomeSponsorLogo.vue';
import { nextContestPractice, nextContest, nextContestEnd } from '@/scripts/contestInfo';
</script>

<template>
    <div class="fullBlock stretchBlock">
        <GlitchText :text="'WWPIT ' + nextContest.getFullYear()" class="contestTitle" font-size="var(--font-title)" color="lime" shadow glow :steps=2 :delay=10 random on-visible></GlitchText>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-row: span 2;">
                <TitledDoubleCutCornerContainer title="General Information" height="100%" align="center" hover-animation="lift" flipped>
                    <p>
                        The West Windsor Plainsboro Informatics Tournament (WWPIT) is a USACO / Codeforces-style programming contest for high school students in which teams of up to 4 compete in 2 rounds of problems across 2 divisions, ranging from AP CSA to USACO Platinum.
                        <br><br>
                        The contest will be held online, on this website, between two divisions: Novice and Advanced.
                        <br><br>
                        <i>Scroll down for more information.</i>
                    </p>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=200 style="grid-column: 1;">
                <TitledDoubleCutCornerContainer :title="'Spring ' + nextContest.getFullYear() " height="100%" align="center" hover-animation="lift">
                    <div class="centered">
                        <GlitchText :text="`${String(nextContest.getMonth() + 1).padStart(2, '0')}/${String(nextContest.getDate()).padStart(2, '0')}/${nextContest.getFullYear()}`" font-size="var(--font-huge)" color="red" glow random flashing :steps=5 start-glitched></GlitchText>
                    </div>
                    <div class="centered" v-if="Date.now() < nextContest.getTime()">
                        <TimerDisplay :to="nextContest" type="clock" font-size="var(--font-large)" color="lime" glow></TimerDisplay>
                    </div>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=300>
                <CutCornerContainer height="100%" hover-animation="lift" flipped vertical-flipped>
                    <CenteredContainer style="font-size: var(--font-20);" v-if="Date.now() < nextContest.getTime()">
                        <GlitchText text="Registrations open!" font-size="var(--font-28)" color="lime" glow flashing random></GlitchText>
                        <div class="centered" style="margin: 8px;">
                            <RouterLink to="/account/registrations" no-deco>
                                <InputLinkButton text="Register" color="lime" font-size="var(--font-large)"></InputLinkButton>
                            </RouterLink>
                        </div>
                        <p style="text-align: center; font-size: var(--font-small);">
                            <i>Scroll down to see contest schedule</i>
                        </p>
                    </CenteredContainer>
                    <CenteredContainer style="font-size: var(--font-20);" v-else-if="Date.now() > nextContestEnd.getTime()">
                        <GlitchText text="Contest ended!" font-size="var(--font-28)" color="red" glow random></GlitchText>
                        <div class="centered" style="margin: 8px;">
                            <RouterLink to="/contest/archive" no-deco>
                                <InputLinkButton text="Archive" color="lime" font-size="var(--font-large)"></InputLinkButton>
                            </RouterLink>
                        </div>
                        <p style="text-align: center">
                            Thanks to all who participated! We hope to see you at the next WWPIT!
                        </p>
                    </CenteredContainer>
                    <CenteredContainer style="font-size: var(--font-20);" v-else>
                        <GlitchText text="Contest started!" font-size="var(--font-28)" color="lime" glow flashing flash-color="red" random></GlitchText>
                        <div class="centered" style="margin: 8px;">
                            <RouterLink to="/contest/contest" no-deco>
                                <InputLinkButton text="Contest" color="lime" font-size="var(--font-large)"></InputLinkButton>
                            </RouterLink>
                        </div>
                        <p style="text-align: center">
                            The contest has not yet started!
                            Join our <a href="https://discord.wwppc.tech">Discord</a> server for important information during the contest!
                        </p>
                    </CenteredContainer>
                </CutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo2"></a>
        <CenteredContainer>
            <GlitchText text="Format & Prizes" font-size="var(--font-title)" color="lime" glow shadow random :steps=2 on-visible></GlitchText>
        </CenteredContainer>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-row: span 2;">
                <TitledDoubleCutCornerContainer title="Prizes (tentative)" height="100%" align="center" hover-animation="lift">
                    <HeaderedTable width="100%" border-color="transparent" header-color="lime" header-background="transparent" style="font-size: var(--font-28); line-height: 0.9em;" :content="{
                        headers: ['Novice', 'Advanced'],
                        data: [
                            [
                                '🥇 $50 + T-shirts',
                                '🥇 $200 + T-shirts'
                            ],
                            [
                                '🥈 $30',
                                '🥈 $150 + T-shirts'
                            ],
                            [
                                '🥉 $30',
                                '🥉 $100 + T-shirts'
                            ]
                        ]
                    }"></HeaderedTable>
                    <p style="font-size: var(--font-28); text-align: center; color: lime; margin: 0px;">
                        X-Camp Prizes (per-person)
                    </p>
                    <HeaderedTable width="100%" border-color="transparent" header-background="transparent" style="font-size: var(--font-28); line-height: 0.7em;" :content="{
                        headers: ['🥇 - $200', '🥈 - $150', '🥉 - $100', '🎁 - $50'],
                        data: []
                    }"></HeaderedTable>
                    <p style="font-size: var(--font-16)">
                        <i>Note: Currently, we can only guarantee prizes to high school students within the US. International transactions are subject to federal law. Other people may compete but may not be able to recieve prizes.</i>
                        <br>
                        <i>X-Camp Prizes are in the form of X-Camp giftcards</i>
                    </p>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=200 style="grid-row: span 2;">
                <TitledDoubleCutCornerContainer title="Contest Format" height="100%" align="center" hover-animation="lift" flipped>
                    <p>
                        WWPIT is a round-based team contest.
                    </p>
                    <ul style="font-size: var(--font-medium);">
                        <li>Two separate timed rounds of eight problems each</li>
                        <li>Instant feedback on submissions</li>
                        <li>Scores based on problems solved, with subtasks</li>
                        <li>Subtask scores are weighted by solve count</li>
                    </ul>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo3]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo3"></a>
        <CenteredContainer>
            <GlitchText text="Schedule" font-size="var(--font-title)" color="lime" glow shadow random :steps=2 on-visible></GlitchText>
        </CenteredContainer>
        <div class="scheduleBlock">
            <AnimateInContainer type="slideUp" show-on-screen>
                <CutCornerContainer height="100%" flipped no-padding hover-animation="lift">
                    <MultipaneSelectorContainer for="contestSchedule">
                        <div class="scheduleHeader">
                            {{ nextContestPractice.toLocaleDateString('en-US', { month: 'long', day: 'numeric' }) }}
                        </div>
                        <MultipaneSelector for="precontest">
                            <div class="scheduleRow">
                                Practice & Testing
                            </div>
                        </MultipaneSelector>
                        <div class="scheduleHeader">
                            {{ nextContest.toLocaleDateString('en-US', { month: 'long', day: 'numeric' }) }} - tentative competition schedule
                        </div>
                        <MultipaneSelector for="openingCeremonies">
                            <div class="scheduleRow">
                                <div>11:00-11:15</div>
                                <div>|</div>
                                <div>Opening ceremonies</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="round1">
                            <div class="scheduleRow">
                                <div>11:30-12:30</div>
                                <div>|</div>
                                <div>Speed Round</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="lunch">
                            <div class="scheduleRow">
                                <div>12:30-1:30</div>
                                <div>|</div>
                                <div>Break</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="round2">
                            <div class="scheduleRow">
                                <div>1:30-4:30</div>
                                <div>|</div>
                                <div>Power Round</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="sponsors">
                            <div class="scheduleRow">
                                <div>4:30-5:30</div>
                                <div>|</div>
                                <div>Sponsor Events</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="closingCeremonies">
                            <div class="scheduleRow">
                                <div>5:30-6:00</div>
                                <div>|</div>
                                <div>Closing Ceremonies</div>
                            </div>
                        </MultipaneSelector>
                        <div class="scheduleRow centered">
                            <i>All times in Eastern Daylight Time</i>
                        </div>
                    </MultipaneSelectorContainer>
                </CutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="min-width: 0px; min-height: 15em;">
                <CutCornerContainer height="100%" vertical-flipped no-padding no-scroll style="font-size: var(--font-medium);" hover-animation="lift">
                    <MultipanePaneContainer for="contestSchedule" default="precontest">
                        <MultipanePane for="precontest">
                            <GlitchText text="Pre-contest Practice & Testing" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Teams will have a chance to test the contest system with a few practice rounds.
                            </p>
                            <p>
                                The practice contest will be open all day. If you wish to enter the practice, you <b>MUST</b> <RouterLink to="/account/registrations">register</RouterLink> for the practice contest <b>1 day</b> before the actual contest!
                            </p>
                        </MultipanePane>
                        <MultipanePane for="openingCeremonies">
                            <GlitchText text="Opening Ceremonies" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Opening and closing ceremonies will be held on our Discord server.
                            </p>
                            <div class="centered">
                                <a href="https://discord.wwppc.tech" target="_blank" style="text-decoration: none;">
                                    <InputIconButton text="Join us on Discord!" img="/img/discord-logo.svg" color="lime" font-size="var(--font-medium)" img-hover-color="#5865F2"></InputIconButton>
                                </a>
                            </div>
                            <p>
                                We'll give more details and instructions on the contest format there.
                            </p>
                        </MultipanePane>
                        <MultipanePane for="round1">
                            <GlitchText text="Speed Round" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                The Speed Round is 60 minutes long with 8 problems. There will be 12 problems in total; Novice will solve the easiest 8; Advanced will solve the hardest 8, with 4 problems shared between divisions.
                            </p>
                        </MultipanePane>
                        <MultipanePane for="lunch">
                            <GlitchText text="Lunch Break" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Be ready to resume the contest <b>10 minutes</b> before the break ends! The contest will resume <b>IMMEDIATELY</b> after lunch!
                            </p>
                        </MultipanePane>
                        <MultipanePane for="round2">
                            <GlitchText text="Power Round" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                The Power Round is 3 hours long with 8 problems. There will be 12 problems in total; Novice will solve the easiest 8; Advanced will solve the hardest 8, with 4 problems shared between divisions.
                            </p>
                        </MultipanePane>
                        <MultipanePane for="sponsors">
                            <GlitchText text="Sponsor Events" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                We will be hosting some events by our sponsors!
                                <br><br>
                                During this time, we will also finalize scores and standings.
                            </p>
                        </MultipanePane>
                        <MultipanePane for="closingCeremonies">
                            <GlitchText text="Closing Ceremonies" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Opening and closing ceremonies will be held on our Discord server!
                            </p>
                            <div class="centered">
                                <a href="https://discord.wwppc.tech" target="_blank" style="text-decoration: none;">
                                    <InputIconButton text="Join us on Discord!" img="/img/discord-logo.svg" color="lime" font-size="var(--font-medium)" img-hover-color="#5865F2"></InputIconButton>
                                </a>
                            </div>
                            <p>
                                We will announce the winners for each division before closing off the contest. If you won a prize, we will contact you shortly ;)
                            </p>
                        </MultipanePane>
                    </MultipanePaneContainer>
                </CutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo4]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo4"></a>
        <div class="centered">
            <GlitchText text="Sponsors" font-size="var(--font-title)" color="lime" glow shadow random :steps=2 on-visible></GlitchText>
        </div>
        <div class="sponsorColumns">
            <div>
                <GlowText text="PARTNERS" font-size="var(--font-huge)" color="lime" shadow></GlowText>
                <HomeSponsorLogo src="/img/cpi-logo.svg" url="https://joincpi.org/" name="CPI Logo" height="12vh"></HomeSponsorLogo>
            </div>
            <div>
                <GlowText text="SILVER" font-size="var(--font-huge)" color="#CCC" shadow></GlowText>
                <HomeSponsorLogo src="/img/hrt-logo.png" url="https://hudsonrivertrading.com/" name="Hudson River Trading Logo" height="10vh"></HomeSponsorLogo>
                <HomeSponsorLogo src="/img/jane-street-logo.png" url="https://janestreet.com/" name="Jane Street Logo" height="9vh"></HomeSponsorLogo>
                <HomeSponsorLogo src="/img/x-camp-logo.png" url="https://x-camp.academy/" name="X-Camp Logo" height="10vh"></HomeSponsorLogo>
                <HomeSponsorLogo src="/img/recursive-dragon-logo.png" url="https://recursivedragon.com/" name="Recursive Dragon Logo" height="10vh"></HomeSponsorLogo>
            </div>
        </div>
        <LineDivider color="#AAA"></LineDivider>
        <div class="sponsors">
            <HomeSponsorLogo src="/img/xyz-logo.svg" url="https://gen.xyz" name=".xyz Logo" height="9vh"></HomeSponsorLogo>
        </div>
        <div class="spacer"></div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo5]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo5"></a>
        <CenteredContainer>
            <GlitchText text="FAQ" font-size="var(--font-title)" color="lime" glow shadow random :steps=2 :delay=10 on-visible></GlitchText>
        </CenteredContainer>
        <div class="faq">
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="When is it?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        WWPIT {{ nextContest.getFullYear() }} will be on <b>{{ nextContest.toLocaleDateString('en-US', { weekday: 'long', month: 'long', day: 'numeric' }) }}</b>, from {{ nextContest.toLocaleTimeString('en-US', { hour: 'numeric', minute: '2-digit' }) }} - {{ nextContestEnd.toLocaleTimeString('en-US', { hour: 'numeric', minute: '2-digit' }) }} EDT.
                        <br><br>
                        <i>Scroll up to see contest schedule</i>
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="How do I compete?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        You can sign up by <b>creating an account and registering <a href="/account/registrations" target="_blank">HERE</a></b>, NO prerequisites needed!
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="Who is eligible for prizes?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        Currently, we can only guarantee prizes to high school students in the United States.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="Where will it be held?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        WWPIT will be held on this website!
                        <br><br>
                        You can register <a href="/account/registrations" target="_blank">here</a> at any time before the contest starts.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="What resources are allowed?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        You may use any resource that was published before the beginning of the contest. Note that this means generative AIs like ChatGPT is disallowed.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="What languages can I use?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        Allowed languages include Java 8, Java 11, Java 17, Java 21, C11, C++11, C++17, C++20, C++23, and Python3.12.3.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="How can I prepare?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        For those experienced in programming, helpful resources include <a href="https://usaco.guide" target="_blank">USACO Guide</a> and <a href="https://codeforces.com" target="_blank">Codeforces</a>.
                        <br><br>
                        To learn C++, see <a href="https://cplusplus.com/doc/tutorial/" target="_blank">CPlusPlus.com</a>. To learn Python, a more beginner-friendly language, the <a href="https://runestone.academy/ns/books/published/thinkcspy/index.html" target="_blank">thinkcspy textbook</a> is useful.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="What is the expected difficulty?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        For the Novice division, expect problems between AP CSA - <a href="https://usaco.org" target="_blank">USACO</a> Gold level.
                        <br><br>
                        For the Advanced division, expect problems between USACO Silver - USACO Platinum level.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
        </div>
        <div class="spacer"></div>
        <ContactFooter></ContactFooter>
    </div>
</template>

<style scoped>
.contestTitle {
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
    flex: 1;
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
    font-size: var(--font-40);
}

.contestWinnerTable>span:nth-child(even) {
    color: lime;
    text-decoration: underline;
    cursor: pointer;
}

.contestWinnerBlock {
    display: flex;
    flex-direction: column;
    font-size: var(--font-32);
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

.scheduleHeader {
    padding: 4px 4px;
    border-bottom: 4px solid white;
    background-color: #222;
    text-align: center;
    font-size: var(--font-medium);
    font-weight: bold;
}

.scheduleRow {
    display: flex;
    flex-direction: row;
    margin: 0px 4px;
    align-items: center;
    font-size: var(--font-20);
    text-wrap: nowrap;
    word-wrap: none;
}

.scheduleRow>div:nth-child(1) {
    text-align: right;
    width: 5.2em;
}

.scheduleRow>div:nth-child(2) {
    font-weight: 900;
    margin: 0px 0.4em;
    color: #AAA;
}

.faq {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(400px, 100%), 1fr));
    grid-auto-flow: dense;
    width: 100%;
    row-gap: 24px;
    column-gap: 24px;
}

ul>li {
    margin-bottom: 0.5em;
}

.spacer {
    flex-grow: 1;
}

.sponsorColumns {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
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
