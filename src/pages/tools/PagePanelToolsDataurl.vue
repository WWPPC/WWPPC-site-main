<script setup lang="ts">
import { TitledCutCornerContainer } from '#/containers';
import { InputCopyButton, InputTextArea, InputFileUpload } from '#/inputs';
import { ref } from 'vue';
import { globalModal } from '#/modal';

const modal = globalModal();

const dataurl = ref('');

const upload = (event: any) => {
    const file: File | undefined = event.target?.files?.item(0);
    if (file == undefined) return;
    const reader = new FileReader();
    reader.onload = () => {
        if (typeof reader.result != 'string') return; // idk should never happen
        if (/^data:image\/(png|jpeg)/.test(reader.result)) {
            dataurl.value = reader.result;
        } else {
            modal.showModal({ title: 'Unsupported file type', content: 'Only .png and .jpg/.jpeg images are allowed.', color: 'red' });
        }
    };
    reader.readAsDataURL(file);
};
</script>

<template>
    <div class="columns">
        <TitledCutCornerContainer title="Image" reversed>
            <img :src="dataurl" class="uploadImg">
            <br>
            <InputFileUpload accept="image/png,image/jpeg" @change=upload></InputFileUpload>
        </TitledCutCornerContainer>
        <TitledCutCornerContainer title="Data URL">
            <InputTextArea v-model="dataurl" resize="vertical" class="big" :disable-typing=true></InputTextArea>
            <InputCopyButton :value="dataurl"></InputCopyButton>
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

.uploadImg {
    box-sizing: border-box;
    max-width: 100%;
    max-height: calc(100% - 32px);
    border: 4px solid white;
}

.big {
    box-sizing: border-box;
    width: 100%;
    height: 20em;
    margin: 0px 0px;
}
</style>