<script setup lang="ts">
import ContactFooter from '#/common/ContactFooter.vue';
import HomeAboutCreditsCard from '#/common-components/home/about/HomeAboutCreditsCard.vue';
import ScrollIndicator from '#/common/ScrollIndicator.vue';
import GlitchSectionTitle from '#/common-components/GlitchSectionTitle.vue';
</script>

<template>
    <div class="fullBlock stretchBlock">
        <GlitchSectionTitle text="Organizers" parallax font-size="var(--font-title)"></GlitchSectionTitle>
        <div class="organizerTable">
            <HomeAboutCreditsCard name="Rishikesh Anabathula" username="wwppc-rishikesh" roles="Lead Organizer<br>WWPPC President<br>Contest Director<br>Problemsetter" img="/img/rishikesh-anabathula.png" grade="Senior (HSS)" codeforces="CutSandstone" github="CutSandstone" discord="559131662143979534" linkedin="rishikesh-anabathula-b621b82a3" bio="USACO Platinum, running enjoyer, AIME qualifier, leetcoder. Likes short biographies, so I made this long sentence for him."></HomeAboutCreditsCard>
            <HomeAboutCreditsCard name="Jie Gao" username="spsquared" roles="Development Lead<br>Website Developer<br>Contest Backend Developer" img="/img/jie-gao.jpg" grade="Senior (HSS)" github="spsquared" discord="587770060462882854" youtube="@sp-squared?sub_confirmation=1" linkedin="jie-gao-518204306" bio="SPARK + SPAARK = win everything. Battlecode 2025 HS 1st & WRO 2023 FE Int. top 4. Made most of the website & servers and maintains backend infrastructure."></HomeAboutCreditsCard>
            <HomeAboutCreditsCard name="Erik Ji" username="erikji" roles="Problemsetter<br>Logistics & Outreach<br>Website Developer" img="/img/erik-ji.jpg" grade="Junior (HSS)" codeforces="passwordisa" github="erikji" discord="688018118492291080" linkedin="erikji" bio="plat,cm,aime,bc25 hs 1st,golf"></HomeAboutCreditsCard>
            <HomeAboutCreditsCard name="Suvanth Erranki" username="susvant" roles="Problemsetter<br>Logistics & Outreach<br>Contest Grading Server Developer" img="/img/suvanth-erranki.jpg" grade="Junior (HSS)" codeforces="susvent" github="Suvanth-Erranki" discord="812014506724556820" bio="USACO Gold Division, MIT Battlecode 2025 HS 1st, (-1 mod Div 1 CF :skull:), also a privacy & security geek sometimes"></HomeAboutCreditsCard>
            <HomeAboutCreditsCard name="Vikram Karamsetty" username="vikramk" roles="Logistics" img="/img/vikram-karamsetty.jpeg" grade="Junior (HSS)" github="VikramKaramsetty" discord="660497297074814976" youtube="@Mangovvk" linkedin="vikram-karamsetty" bio="avid programmer (usaco silver), dedicated roboticist (First Tech Challenge #14481), track runner, problem solver, and engineer!"></HomeAboutCreditsCard>
        </div>
        <div class="spacer"></div>
        <ScrollIndicator anchor="a[name=pageAboutScrollTo]"></ScrollIndicator>
    </div>
    <div>
        <a name="pageAboutScrollTo"></a>
        <GlitchSectionTitle text="Junior Organizers" font-size="var(--font-small-title)"></GlitchSectionTitle>
        <div class="organizerTable organizerTableSmall">
            <HomeAboutCreditsCard name="Chris Ren" username="chrispyhackerace" roles="Logistics & Outreach<br>Website Developer" img="/img/chris-ren.jpg" grade="Freshman (HSS)" github="chrispyhackingace" discord="706203796774322278" linkedin="christopher-ren-67a967314" website="instagram.com/chrispyhackingace/" bio="already has his ED to MIT." width="273px" height="350px"></HomeAboutCreditsCard>
            <HomeAboutCreditsCard name="Siddharth Goli" username="rawbill" roles="Junior Dev" img="/img/internet-icon.svg" grade="Freshman (HSS)" codeforces="siddharthgoli" github="rawbill" discord="1238666673884500024" bio="USACO Bronze<br></br>First Tech Challenge #23490" width="273px" height="350px"></HomeAboutCreditsCard>
            <HomeAboutCreditsCard name="Prahalad Setty" username="toazty" roles="Website Developer" img="/img/setty.png" grade="Freshman (HSS)" codeforces="toazty" github="prahaladsetty" discord="751894068266795118" bio="FRC + coding" width="273px" height="350px"></HomeAboutCreditsCard>
            <HomeAboutCreditsCard name="Syam Paladugu" username="reverseflash" roles="Logistics & Outreach" img="/img/internet-icon.svg" grade="Freshman (HSS)" codeforces="reverseFlash123" discord="751894068266795118" bio="FTC #23490<br></br> FRC #1923" width="273px" height="350px"></HomeAboutCreditsCard>
        </div>
    </div>
    <div>
        <GlitchSectionTitle text="Problem Testers" font-size="var(--font-small-title)"></GlitchSectionTitle>
        <div class="organizerTable problemTesterTable">
            <h3>William Yuan</h3>
            <h3>Advik Vermani</h3>
        </div>
    </div>
    <div>
        <GlitchSectionTitle text="Alumni" font-size="var(--font-small-title)"></GlitchSectionTitle>
        <div class="organizerTable organizerTableSmall">
            <HomeAboutCreditsCard name="Maitian Sha" username="sp" roles="Problemsetter" img="/img/maitian-sha.jpg" grade="Junior (HSS)" codeforces="spuh" aops="452171" github="SampleProvider" discord="706967946198777867" website="youtube.com/watch?v=dQw4w9WgXcQ" bio="USACO Plat, USAMO, 6x AIME, 2x WRO Future Engineers Internationals Top 4, Battlecode 2025 HS 1st place, also Block Pushing Game." width="273px" height="350px"></HomeAboutCreditsCard>
        </div>
        <ContactFooter></ContactFooter>
    </div>
</template>

<style scoped>
.organizerTable {
    display: grid;
    --table-size: 320px;
    grid-template-columns: repeat(auto-fit, minmax(var(--table-size), 1fr));
    width: 100%;
    justify-items: center;
    row-gap: 24px;
    column-gap: 24px;
}

.organizerTableSmall {
    --table-size: 273px;
}

.problemTesterTable {
    --table-size: 200px;
}

.spacer {
    flex-grow: 1;
}
</style>
