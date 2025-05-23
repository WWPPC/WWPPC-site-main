<script setup lang="ts">
import { MultipaneSelectorContainer, MultipaneSelector, MultipanePaneContainer, MultipanePane } from '#/multipane';
import { AnimateInContainer, CenteredContainer, TitledDoubleCutCornerContainer, CutCornerContainer, TitledCollapsibleContainer, HeaderedTable } from '#/containers';
import ContactFooter from '#/common/ContactFooter.vue';
import ScrollIndicator from '#/common/ScrollIndicator.vue';
import { InputLinkButton, InputIconButton } from '#/inputs';
import { GlitchText, GlowText } from '#/text';
import TimerDisplay from '#/common/TimerDisplay.vue';
import SponsorList from '#/common-components/SponsorList.vue';
import GlitchSectionTitle from '#/common-components/GlitchSectionTitle.vue';
const contest = new Date('6/2/2024 9:30 AM EST');
const contestEnd = new Date('6/2/2024 5:00 PM EST');

const sponsors = {
    partner: [
        { name: "CPI Logo", src: "/img/cpi-logo.svg", url: "https://joincpi.org/", height: "12vh" }
    ],
    gold: [
        { name: "X-Camp Logo", src: "/img/x-camp-logo.png", url: "https://x-camp.academy/", height: "10vh" }
    ],
    silver: [
        { name: "ICode Logo", src: "/img/icode-logo.png", url: "https://icodeschool.com/", height: "10vh" }
    ],
    bronze: [
        { name: "Desmos Logo", src: "/img/desmos-logo.svg", url: "https://desmos.com/", height: "5.5vh" },
        { name: "AoPS Logo", src: "/img/aops-logo.svg", url: "https://artofproblemsolving.com/", height: "12vh" },
        { name: ".xyz Logo", src: "/img/xyz-logo.svg", url: "https://gen.xyz", height: "9vh" },
        { name: "Echo3D Logo", src: "/img/echo3d-logo.png", url: "https://www.echo3d.com/", height: "5.5vh" },
        { name: "Axure Logo", src: "/img/axure-logo.svg", url: "https://axure.com/", height: "6vh" }
    ]
};

</script>

<template>
    <div class="fullBlock stretchBlock">
        <GlitchSectionTitle text="WWPIT 2024" parallax font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-row: span 2;">
                <TitledDoubleCutCornerContainer title="General Information" height="100%" align="center" hover-animation="lift" flipped>
                    <p>
                        The WWP Informatics Tournament (WWPIT) is a USACO / Codeforces-style programming contest for high school students in which teams of up to 4 compete in 3 rounds of problems across 2 divisions, ranging from AP CSA to USACO Platinum.
                        <br><br>
                        The contest will be held online, on this website, between two divisions: Novice and Advanced.
                        <br><br>
                        <i>Scroll down for more information.</i>
                    </p>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=200 style="grid-column: 1;">
                <TitledDoubleCutCornerContainer title="Spring 2024" height="100%" align="center" hover-animation="lift">
                    <div class="centered">
                        <GlitchText text="06/02/2024" font-size="var(--font-huge)" color="red" glow random flashing :steps=5 start-glitched></GlitchText>
                    </div>
                    <div class="centered" v-if="Date.now() < contest.getTime()">
                        <TimerDisplay :to="contest" type="clock" font-size="var(--font-large)" color="lime" glow></TimerDisplay>
                    </div>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=300>
                <CutCornerContainer height="100%" hover-animation="lift" flipped vertical-flipped>
                    <CenteredContainer style="font-size: var(--font-20);">
                        <GlitchText text="Contest ended!" font-size="var(--font-28)" color="red" glow random></GlitchText>
                        <div class="centered" style="margin: 8px;">
                            <RouterLink to="/contest/upsolve" no-deco>
                                <InputLinkButton text="Upsolve" color="lime" font-size="var(--font-large)"></InputLinkButton>
                            </RouterLink>
                        </div>
                        <p style="text-align: center">
                            Thanks to all who participated! We hope to see you in the WWPIT Fall 2024!
                        </p>
                    </CenteredContainer>
                </CutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo"></a>
        <GlitchSectionTitle text="Winners" font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="contestInfoBlock winnersBlock">
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
            <AnimateInContainer type="slideUp" show-on-screen :delay=100>
                <TitledDoubleCutCornerContainer title="Advanced" height="100%" align="center" hover-animation="lift">
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
            <AnimateInContainer type="slideUp" show-on-screen :delay=400>
                <CutCornerContainer title="" height="100%" align="center" hover-animation="lift" flipped vertical-flipped>
                    <div class="centered">
                        <GlowText text="Congratulations to our winners!" color="lime" font-size="var(--font-large)" glow shadow></GlowText>
                    </div>
                    <p style="text-align: center;">
                        Also thanks to everyone for sticking through our first contest with us! We are taking feedback and are making lots of changes for our fall contest!
                    </p>
                </CutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo2]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo2"></a>
        <GlitchSectionTitle text="Format & Prizes" font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-row: span 2;">
                <TitledDoubleCutCornerContainer title="Prizes" height="100%" align="center" hover-animation="lift">
                    <HeaderedTable width="100%" border-color="transparent" header-color="lime" header-background="transparent" style="font-size: var(--font-28); line-height: 0.9em;" :content="{
                        headers: ['Novice', 'Advanced'],
                        data: [
                            [
                                '🥇 $30 + T-shirts',
                                '🥇 $150 + T-shirts'
                            ],
                            [
                                '🥈 $10 + T-shirts',
                                '🥈 $100 + T-shirts'
                            ],
                            [
                                '🥉 $10 + T-shirts',
                                '🥉 $50 + T-shirts'
                            ]
                        ]
                    }"></HeaderedTable>
                    <p style="font-size: var(--font-28); text-align: center; color: lime; margin: 0px;">
                        X-Camp Prizes (per-person)
                    </p>
                    <HeaderedTable width="100%" border-color="transparent" header-background="transparent" style="font-size: var(--font-28); line-height: 0.7em;" :content="{
                        headers: ['🥇 - $200', '🥈 - $150', '🥉 - $100'],
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
                        WWPIT is a round-based team contest, where problems are revealed as time progresses.
                    </p>
                    <ul style="font-size: var(--font-medium);">
                        <li>Three separate timed rounds of 6 problems</li>
                        <li>Instant feedback on submissions</li>
                        <li>Scores based on problems solved, with subtasks</li>
                        <li>Subtask scores are weighted by the number of people who solved</li>
                    </ul>
                </TitledDoubleCutCornerContainer>
            </AnimateInContainer>
        </div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo3]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo3"></a>
        <GlitchSectionTitle text="Schedule" font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="scheduleBlock">
            <AnimateInContainer type="slideUp" show-on-screen>
                <CutCornerContainer height="100%" flipped no-padding hover-animation="lift">
                    <MultipaneSelectorContainer for="contestSchedule">
                        <div class="scheduleHeader">
                            June 1
                        </div>
                        <MultipaneSelector for="precontest">
                            <div class="scheduleRow">
                                Practice & Testing
                            </div>
                        </MultipaneSelector>
                        <div class="scheduleHeader">
                            June 2
                        </div>
                        <MultipaneSelector for="openingCeremonies">
                            <div class="scheduleRow">
                                <div>10:15-10:45</div>
                                <div>|</div>
                                <div>Opening ceremonies</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="round1">
                            <div class="scheduleRow">
                                <div>11:00-12:00</div>
                                <div>|</div>
                                <div>Round 1</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="lunch">
                            <div class="scheduleRow">
                                <div>12:00-1:00</div>
                                <div>|</div>
                                <div>Lunch break</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="round2">
                            <div class="scheduleRow">
                                <div>1:00-2:00</div>
                                <div>|</div>
                                <div>Round 2</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="round3">
                            <div class="scheduleRow">
                                <div>2:10-3:30</div>
                                <div>|</div>
                                <div>Round 3</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="sponsors">
                            <div class="scheduleRow">
                                <div>3:40-4:40</div>
                                <div>|</div>
                                <div>Sponsor Events</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="closingCeremonies">
                            <div class="scheduleRow">
                                <div>4:55-5:30</div>
                                <div>|</div>
                                <div>Closing ceremonies</div>
                            </div>
                        </MultipaneSelector>
                    </MultipaneSelectorContainer>
                </CutCornerContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="min-width: 0px; min-height: 15em;">
                <CutCornerContainer height="100%" vertical-flipped no-padding no-scroll style="font-size: var(--font-medium);" hover-animation="lift">
                    <MultipanePaneContainer for="contestSchedule" default="precontest">
                        <MultipanePane for="precontest">
                            <GlitchText text="Pre-contest Practice & Testing" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Teams (including the WWPPC team) will have a chance to test the contest system with a few practice rounds.
                            </p>
                            <p>
                                The practice contest will be open all day. If you wish to enter the practice, you <b>MUST </b>
                                <RouterLink to="/account/registrations">register</RouterLink> for the practice contest <b>1 day</b> before the actual contest!
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
                            </p>
                        </MultipanePane>
                        <MultipanePane for="openingCeremonies">
                            <GlitchText text="Opening Ceremonies" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Opening and closing ceremonies will be held on our Discord server!
                            </p>
                            <div class="centered">
                                <a href="https://discord.wwppc.tech" target="_blank" style="text-decoration: none;">
                                    <InputIconButton text="Join us on Discord!" img="/img/discord-logo.svg" color="lime" font-size="var(--font-medium)" img-hover-color="#5865F2"></InputIconButton>
                                </a>
                            </div>
                            <p>
                                We'll give more details and instructions on the contest format there.
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
                            </p>
                        </MultipanePane>
                        <MultipanePane for="round1">
                            <GlitchText text="Round 1" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Round 1 is 60 minutes long with 6 problems. Novice and Advanced divisions may or may not share problems.
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
                            </p>
                        </MultipanePane>
                        <MultipanePane for="lunch">
                            <GlitchText text="Lunch Break" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Lunch is one hour long and we'll be hosting some fun events during the break!
                                <br><br>
                                However, be ready to resume the contest <b>10 minutes</b> before the break ends! The contest will resume <b>IMMEDIATELY</b> after lunch!
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
                            </p>
                        </MultipanePane>
                        <MultipanePane for="round2">
                            <GlitchText text="Round 2" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Round 2 is 60 minutes long with 6 problems. Novice and Advanced divisions may or may not share problems.
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
                            </p>
                        </MultipanePane>
                        <MultipanePane for="round3">
                            <GlitchText text="Round 3" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                Round 3 is 80 minutes long with 6 problems. Novice and Advanced divisions may or may not share problems.
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
                            </p>
                        </MultipanePane>
                        <MultipanePane for="sponsors">
                            <GlitchText text="Sponsor Events" font-size="var(--font-28)" color="lime" on-visible></GlitchText>
                            <p>
                                We will be hosting some events by our sponsors!
                                <br><br>
                                During this time, we will also finalize scores and determine the standings.
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
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
                                We will announce the winners for each division before closing off the contest.
                            </p>
                            <p style="font-size: var(--font-16)">
                                <i>All times are in Eastern Standard Time (daylight savings)</i>
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
        <SponsorList color="lime" :partners="sponsors.partner" :gold="sponsors.gold" :silver="sponsors.silver" :bronze="sponsors.bronze" />
        <div class="spacer"></div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo5]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo5"></a>
        <GlitchSectionTitle text="FAQ" font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="faq">
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="When is it?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        WWPIT 2024 will be on <b>Sunday, June 2</b>, from 10:15 AM - 5:30 PM EST.
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
                        You can use any resource that was published before the beginning of the contest.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsible title="What languages can I use?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        Allowed languages include Java 8, Java 11, Java 17, Java 21, C11, C++11, C++17, C++20, and Python3.12.3.
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
                        For the Novice division, expect problems within the <a href="https://usaco.org" target="_blank">USACO</a> Bronze-upper USACO Silver division. For the Advanced division, expect problems within the USACO Silver-USACO Platinum division.
                    </p>
                </TitledCollapsible>
            </AnimateInContainer>
        </div>
        <div class="spacer"></div>
        <ContactFooter></ContactFooter>
    </div>
</template>

<style scoped>
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
</style>