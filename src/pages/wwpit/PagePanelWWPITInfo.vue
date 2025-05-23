<script setup lang="ts">
import { MultipaneSelectorContainer, MultipaneSelector, MultipanePaneContainer, MultipanePane } from '#/multipane';
import { AnimateInContainer, CenteredContainer, TitledDoubleCutCornerContainer, CutCornerContainer, TitledCollapsibleContainer, HeaderedTable } from '#/containers';
import ContactFooter from '#/common/ContactFooter.vue';
import ScrollIndicator from '#/common/ScrollIndicator.vue';
import { InputLinkButton, InputIconButton } from '#/inputs';
import { GlitchText } from '#/text';
import TimerDisplay from '#/common/TimerDisplay.vue';
import SponsorList from '#/common-components/SponsorList.vue';
import { nextContestPractice, nextContest, nextContestEnd } from '@/scripts/contestInfo';
import GlitchSectionTitle from '#/common-components/GlitchSectionTitle.vue';

const sponsors = {
    partner: [
        { name: "CPI Logo", src: "/img/cpi-logo.svg", url: "https://joincpi.org/", height: "12vh" }
    ],
    gold: [
        
    ],
    silver: [
        { name: "Hudson River Trading Logo", src: "/img/hrt-logo.svg", url: "https://hudsonrivertrading.com/", height: "10vh" },
        { name: "Jane Street Logo", src: "/img/jane-street-logo.svg", url: "https://janestreet.com/", height: "10vh" },
        { name: "X-Camp Logo", src: "/img/x-camp-logo.png", url: "https://x-camp.academy/", height: "10vh" },
        { name: "Recursive Dragon", src: "/img/recursive-dragon-logo.png", url:"https://recursivedragon.com", height: "10vh"}
    
    ],
    bronze: [
        { name: ".xyz Logo", src: "/img/xyz-logo.svg", url: "https://gen.xyz", height: "9vh" }
    ]
};

</script>

<template>
    <div class="fullBlock stretchBlock">
        <GlitchSectionTitle :text="'WWPIT ' + nextContest.getFullYear()" parallax font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="contestInfoBlock">
            <AnimateInContainer type="slideUp" show-on-screen :delay=100 style="grid-row: span 2;">
                <TitledDoubleCutCornerContainer title="General Information" height="100%" align="center" hover-animation="lift" flipped>
                    <p>
                        The West Windsor Plainsboro Informatics Tournament (WWPIT) is a USACO / Codeforces-style programming contest in which teams of up to 4 compete in 2 rounds of problems across 2 divisions, ranging from AP CSA to USACO Platinum. All are encouraged to participate.
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
                        <GlitchText :text="nextContest.toLocaleDateString(undefined, { month: '2-digit', day: '2-digit', year: 'numeric'})" font-size="var(--font-huge)" color="red" glow random flashing :steps=5 start-glitched></GlitchText>
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
        <GlitchSectionTitle text="Format & Prizes" font-size="var(--font-title)"></GlitchSectionTitle>
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
                                '🥈 $150'
                            ],
                            [
                                '🥉 $30',
                                '🥉 $100'
                            ],
                            [
                                '4. $20',
                                '4. $50'
                            ],
                            [
                                '5. $20',
                                '5. $50'
                            ]
                            
                        ]
                    }"></HeaderedTable>
                    <p style="font-size: var(--font-28); text-align: center; color: lime; margin: 0px;">
                        X-Camp Prizes (per-person)
                    </p>
                    <HeaderedTable width="100%" border-color="transparent" header-background="transparent" style="font-size: var(--font-28); line-height: 0.7em;" :content="{
                        headers: ['🥇 - $200', '🥈 - $150', '🥉 - $100', 'All - $50'],
                        data: []
                    }"></HeaderedTable>
                    <p style="font-size: var(--font-16)">
                        <i>Note: Currently, we can only guarantee prizes to pre-college students within the US. International transactions are subject to federal law. Other people may compete but may not be able to recieve prizes.</i>
                        <br>
                        <i>X-Camp Prizes are in the form of X-Camp class coupons.</i>
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
                        <li>Scores based on number of problems solved</li>
                        <li>Penalty based on number of wrong submissions and last correct submission</li>
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
                            {{ nextContestPractice.toLocaleDateString(undefined, { month: 'long', day: 'numeric' }) }}
                        </div>
                        <MultipaneSelector for="precontest">
                            <div class="scheduleRow">
                                Practice & Testing
                            </div>
                        </MultipaneSelector>
                        <div class="scheduleHeader">
                            {{ nextContest.toLocaleDateString(undefined, { month: 'long', day: 'numeric' }) }}
                        </div>
                        <MultipaneSelector for="openingCeremonies">
                            <div class="scheduleRow">
                                <div>{{ new Date("4/19/2025 12:30 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}-{{ new Date("4/19/2025 12:45 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}</div>
                                <div>|</div>
                                <div>Opening Ceremony</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="round1">
                            <div class="scheduleRow">
                                <div>{{ new Date("4/19/2025 1:00 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}-{{ new Date("4/19/2025 2:00 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}</div>
                                <div>|</div>
                                <div>Speed Round</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="lunch">
                            <div class="scheduleRow">
                                <div>{{ new Date("4/19/2025 2:00 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}-{{ new Date("4/19/2025 3:00 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}</div>
                                <div>|</div>
                                <div>Break</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="round2">
                            <div class="scheduleRow">
                                <div>{{ new Date("4/19/2025 3:00 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}-{{ new Date("4/19/2025 6:00 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}</div>
                                <div>|</div>
                                <div>Power Round</div>
                            </div>
                        </MultipaneSelector>
                        <MultipaneSelector for="closingCeremonies">
                            <div class="scheduleRow">
                                <div>{{ new Date("4/19/2025 7:00 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}-{{ new Date("4/19/2025 7:15 PM EDT").toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }}</div>
                                <div>|</div>
                                <div>Closing Ceremony</div>
                            </div>
                        </MultipaneSelector>
                        <div class="scheduleRow centered">
                            <i>All times in {{ new Intl.DateTimeFormat(undefined, { timeZoneName: 'long'}).formatToParts(new Date()).find(part => part.type === 'timeZoneName')!.value }}</i>
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
                                Teams will have a chance to test the contest system with a practice round.
                            </p>
                            <p>
                                The practice contest will be open all day. To enter the practice, you <b>MUST</b> <RouterLink to="/account/registrations">register</RouterLink> for the practice contest <b>1 day</b> before the actual contest!
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
        <SponsorList 
            color="lime"
            :partners="sponsors.partner" 
            :gold="sponsors.gold" 
            :silver="sponsors.silver" 
            :bronze="sponsors.bronze"
        />
        <div class="spacer"></div>
        <ScrollIndicator anchor="a[name=pageContestScrollTo5]"></ScrollIndicator>
    </div>
    <div class="fullBlock stretchBlock">
        <a name="pageContestScrollTo5"></a>
        <GlitchSectionTitle text="FAQ" font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="faq">
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="When is it?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        WWPIT {{ nextContest.getFullYear() }} will be on <b>{{ nextContest.toLocaleDateString(undefined, { weekday: 'long', month: 'long', day: 'numeric' }) }}</b>, from {{ nextContest.toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }} to {{ nextContestEnd.toLocaleTimeString(undefined, { hour: 'numeric', minute: '2-digit' }) }} ({{ new Intl.DateTimeFormat(undefined, { timeZoneName: 'long'}).formatToParts(new Date()).find(part => part.type === 'timeZoneName')!.value }}).
                        <br><br>
                        <i>Scroll up to see contest schedule</i>
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="How do I compete?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        You can sign up by <b>creating an account and registering <a href="/account/registrations" target="_blank">HERE</a></b>, NO prerequisites needed!
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="Who is eligible for prizes?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        Currently, we can only guarantee prizes to pre-college students in the United States.
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="Where will it be held?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        WWPIT will be held on this website!
                        <br><br>
                        You can register <a href="/account/registrations" target="_blank">here</a> at any time before the contest starts.
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="What resources are allowed?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        You may use any resource that was published before the beginning of the contest. Note that this means generative AIs like ChatGPT is disallowed.
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="What languages can I use?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        Allowed languages include Java 8, Java 11, Java 17, Java 21, C11, C++11, C++17, C++20, C++23, and Python3.12.3.
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="How can I prepare?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        For those experienced in programming, helpful resources include <a href="https://usaco.guide" target="_blank">USACO Guide</a> and <a href="https://codeforces.com" target="_blank">Codeforces</a>.
                        <br><br>
                        To learn C++, see <a href="https://cplusplus.com/doc/tutorial/" target="_blank">CPlusPlus.com</a>. To learn Python, a more beginner-friendly language, the <a href="https://runestone.academy/ns/books/published/thinkcspy/index.html" target="_blank">thinkcspy textbook</a> is useful.
                    </p>
                </TitledCollapsibleContainer>
            </AnimateInContainer>
            <AnimateInContainer type="slideUp" show-on-screen>
                <TitledCollapsibleContainer title="What is the expected difficulty?" startCollapsed>
                    <p style="font-size: var(--font-20)">
                        For the Novice division, expect problems between AP CSA - <a href="https://usaco.org" target="_blank">USACO</a> Gold level.
                        <br><br>
                        For the Advanced division, expect problems between USACO Silver - USACO Platinum level.
                    </p>
                </TitledCollapsibleContainer>
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
    width: 8em;
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
