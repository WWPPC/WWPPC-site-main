<script setup lang="ts">
import { TitledCutCornerContainer } from '#/containers';
import { InputFileUpload } from '#/inputs';
import { ref, watch } from 'vue';
import { globalModal } from '#/modal';
import InputButton from '#/inputs/InputButton.vue';
import InputSlider from '#/inputs/InputSlider.vue';
import { throttle } from '#/util/inputLimiting';

const modal = globalModal();

const original = ref('');
const converted = ref('');

const rotate = ref(0);
const hue = ref(0);
const saturation = ref(100);
const contrast = ref(100);
const brightness = ref(100);
const blur = ref(0);
const opacity = ref(100);

const draw = () => {
    if (original.value === '') return;
    const img = new Image();
    img.src = original.value;
    img.onload = () => {
        const canvas = document.createElement('canvas');
        canvas.width = img.width;
        canvas.height = img.height;
        const ctx = canvas.getContext('2d');
        if (!ctx) { // idk it gives an error without this (i clicked on the lightbulb and it did this)
            return modal.showModal({title: 'Unsopported image', content:'Try again or use another image.', color: 'red'}); //idk how this would happen
        }
        ctx.filter = `
          brightness(${brightness.value}%) 
          contrast(${contrast.value}%) 
          saturate(${saturation.value}%) 
          hue-rotate(${hue.value}deg) 
          blur(${blur.value}px) 
          opacity(${opacity.value}%)
        `;
        ctx.drawImage(img, 0, 0, img.width, img.height);
        converted.value = canvas.toDataURL('image/png');
    }
}

const upload = (event: any) => {
    const file: File | undefined = event.target?.files?.item(0);
    if (file == undefined) return;
    const reader = new FileReader();

    reader.onload = () => {
        if (typeof reader.result != 'string') return; // idk should never happen
        original.value = reader.result;
         draw();
        if (file.type == 'video/mp4' || file.type == 'video/mov' || file.type == 'video/AVI') { //prevents videos from loading
            modal.showModal({ title: 'Unsupported file type', content: 'Only images are allowed.', color: 'red' });
        }
    };
    reader.readAsDataURL(file);
};

const resetFilters = () => {

    draw();
    
    return rotate.value = 0, 
    hue.value = 0,
    saturation.value = 100,
    contrast.value = 100,
    brightness.value = 100,
    blur.value = 0,
    opacity.value = 100;

}
watch([brightness, contrast, saturation, hue, blur, opacity], throttle(() => draw(), 1000));


const applyFilter = () => {
    draw();
}

</script>

<template>
    <div class="columns"> 
        <TitledCutCornerContainer title="Image" reversed>
            <img :src="converted" class="uploadImg">
            <br>
            <InputFileUpload class="align" accept="image/png+xml" @change=upload></InputFileUpload>
        </TitledCutCornerContainer>
        <TitledCutCornerContainer title="Filters">
            <div class="flexbox">
                <p>Hue: {{ hue }}</p>
                <InputSlider v-model="hue" :min="0" :max="360" ></InputSlider>
                <p>Saturation: {{ saturation }}</p>
                <InputSlider v-model="saturation" :min="0" :max="200" ></InputSlider>
                <p>Contrast: {{ contrast }}</p>
                <InputSlider v-model="contrast" :min="100" :max="200" ></InputSlider>
                <p>Brightness: {{ brightness }}</p>
                <InputSlider v-model="brightness" :min="100" :max="200" ></InputSlider>
                <p>Opacity: {{ opacity }}</p>
                <InputSlider v-model="opacity" :min="0" :max="100" ></InputSlider>
                <p>Blur: {{ blur }}</p>
                <InputSlider v-model="blur" :min="0" :max="10" :step="0.1" ></InputSlider>
                <InputButton text="Apply Filters" color="Green" @click="applyFilter"></InputButton>
                <InputButton class="buttonpad" text="Reset Filters" color="Red" @click="resetFilters"></InputButton>
            </div>
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

.align {
    display: block;
    margin-left: 0%; 
}

.uploadImg {
    box-sizing: border-box;
    max-width: 100%;
    max-height: calc(100% - 32px);
    border: 4px solid white;
    background-color: black;
    background-image:
        linear-gradient(45deg, #222 25%, transparent 25%),
        linear-gradient(135deg, #222 25%, transparent 25%),
        linear-gradient(45deg, transparent 75%, #222 75%),
        linear-gradient(135deg, transparent 75%, #222 75%);
    background-size: 20px 20px;
    background-position: 0 0, 10px 0, 10px -10px, 0px 10px;
    display: block;
    margin-left: auto;
    margin-right: auto;
    width: auto;   
}

.big {
    box-sizing: border-box;
    width: 100%;
    height: 20em;
    margin: 0px 0px;
}

.flexbox {
    display: flex;
    flex-direction: column;
}

.buttonpad {
    margin-top: 15px;
}

</style>