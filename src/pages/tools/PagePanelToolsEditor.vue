<script setup lang="ts">
import { TitledCutCornerContainer } from '#/containers';
import { InputTextArea } from '#/inputs';
import { onMounted, ref, watch } from 'vue';
import latexify from '#/util/katexify';

const html = ref('');
const rendered = ref('');
onMounted(() => {
    if (localStorage.getItem('problemEditorSaved') != null) html.value = localStorage.getItem('problemEditorSaved')!;
});
watch(html, () => {
    localStorage.setItem('problemEditorSaved', html.value);
    latexify(html.value).then((html) => rendered.value = html);
});
</script>

<template>
    <div class="columns">
        <TitledCutCornerContainer title="LaTeX/HTML" reversed>
            <InputTextArea v-model="html" resize="none" class="big"></InputTextArea>
        </TitledCutCornerContainer>
        <TitledCutCornerContainer title="Rendered">
            <div v-html="rendered" class="render"></div>
        </TitledCutCornerContainer>
    </div>
</template>

<style scoped>
.columns {
    display: grid;
    height: 100%;
    grid-template-columns: 1fr 1fr;
    column-gap: 24px;
}

.big {
    box-sizing: border-box;
    width: 100%;
    height: calc(100% - 4px);
    margin: 0px 0px;
    border: none;
}

.render {
    font-size: var(--font-small);
    text-align: justify;
}
</style>