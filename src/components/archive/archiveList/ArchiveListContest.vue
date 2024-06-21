<script setup lang="ts">
import { autoGlitchTextTransition } from '#/text';
import { AnimateInContainer, CutCornerContainer } from '#/containers';
import ArchiveListRound from './ArchiveListRound.vue';
import OnScreenHook from '#/common/OnScreenHook.vue';
import { useRouter } from 'vue-router';
import { ref } from 'vue';
import { useUpsolveManager, type UpsolveContest } from '@/scripts/UpsolveManager';
import { globalModal } from '#/modal';

const props = defineProps<{
    id: string
}>();

const modal = globalModal();
const router = useRouter();
const upsolveManager = useUpsolveManager();

const contest = ref<UpsolveContest>();
const titleText = autoGlitchTextTransition(() => contest.value?.id ?? '', 40, 1, 10, 2);

const navContest = () => {
    router.push('/contest/archive/' + contest.value?.id);
};

let loaded = false;
const load = async () => {
    if (loaded) return;
    loaded = true;
    const data = await upsolveManager.getContestData(props.id);
    if (data instanceof Error) {
        modal.showModal({ title: data.message, content: `Could not load contest (loading "${props.id}")`, color: 'red' });
        return;
    }
    contest.value = data;
}
</script>

<template>
    <CutCornerContainer style="margin-bottom: 16px;" no-padding no-scroll>
        <OnScreenHook @visible="load()"></OnScreenHook>
        <div class="archiveContestHeader" @click="navContest()">
            <h2>{{ titleText }}</h2>
        </div>
        <AnimateInContainer type="fade" v-for="(round, index) in contest?.rounds" :key="round.number" :delay="index * 100">
            <ArchiveListRound :data="round" minimized></ArchiveListRound>
        </AnimateInContainer>
    </CutCornerContainer>
</template>

<style scoped>
.archiveContestHeader {
    box-sizing: border-box;
    width: 100%;
    padding: 8px 12px;
    border-bottom: 4px solid white;
    background-color: #333;
    color: lime;
    text-decoration: underline;
    cursor: pointer;
}
</style>
