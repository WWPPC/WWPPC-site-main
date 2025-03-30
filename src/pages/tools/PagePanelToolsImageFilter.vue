<script setup lang="ts">
import { TitledCutCornerContainer } from '#/containers';
import { InputFileUpload, InputNumberBox } from '#/inputs';
import { ref, watch, computed } from 'vue';
import { globalModal } from '#/modal';
import InputButton from '#/inputs/InputButton.vue';

const modal = globalModal();

const scale = ref(1);
const width = ref(0);
const height = ref(0);
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
    if (original.value == '') return;
    const img = new Image();
    img.src = original.value;
    img.onload = () => {
        const canvas = document.createElement('canvas');
        width.value = img.width;
        height.value = img.height;
        canvas.width = img.width;
        canvas.height = img.height;
        const ctx = canvas.getContext('2d');
        ctx?.drawImage(img, 0, 0, img.width, img.height);
        converted.value = canvas.toDataURL('image/png');
    };
};

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

const imgStyle = computed(() => { //computed() is a cache to make program faster
    return {
    transform: `rotate(${rotate.value}deg) scale(${scale.value})`,  //instead of using watch(scale, draw), utilizing the css filter scale reduces lag by a lot.
    filter: `
          brightness(${brightness.value}%) 
          contrast(${contrast.value}%)
          saturate(${saturation.value}%)
          hue-rotate(${hue.value}deg)
          blur(${blur.value}px)
          opacity(${opacity.value}%)
        `
    };
    
});

const reset_filters = () => {

   return rotate.value = 0, 
   hue.value = 0,
   saturation.value = 100,
   contrast.value = 100,
   brightness.value = 100,
   blur.value = 0,
   opacity.value = 100,
   scale.value = 1;
 
}

</script>

<template>
    <div class="columns"> 
        <TitledCutCornerContainer title="Image" reversed>
            <img :src="converted" class="uploadImg" :style="imgStyle">
            <br>
            <InputFileUpload class="align" accept="image/png+xml" @change=upload></InputFileUpload>
            <br>
        </TitledCutCornerContainer>
        <TitledCutCornerContainer title="Filters">
            <div>
                Scale: 
                <br/>
                <InputNumberBox v-model="scale" :default-value="1" :step="0.1" :min="-5" :max="5"></InputNumberBox>
            </div>
            <br>
            <div>
                Rotate:
                <input v-model="rotate" type="range" min="0" max="360" class="slider" />
                <br/>
                <InputNumberBox v-model="rotate" :step="1"></InputNumberBox>
            </div>
            <br>
            <div>
                Hue:
                <input v-model="hue" type="range" min="0" max="360" class="slider" />
                <br />
                <InputNumberBox v-model="hue" :step="1"></InputNumberBox>
            </div>
            <br>
            <div>
                Saturation:
                <input v-model="saturation"  type="range" min="0" max="200" class="slider" />
                <br />
                <InputNumberBox  v-model="saturation" :step="1"></InputNumberBox>
            </div>
            <br>
            <div>
                Contrast:
                <input v-model="contrast" type="range"  min="0" max="200" class="slider" />
                <br />
                <InputNumberBox v-model="contrast" :step="1"></InputNumberBox>
            </div>
            <br>
            <div>
                Brightness:
                <input v-model="brightness" type="range"  min="0" max="200" class="slider" />
                <br />
                <InputNumberBox v-model="brightness" :step="1"></InputNumberBox>
            </div>
            <br>
            <div>
                Opacity:
                <input v-model="opacity" type="range"  min="0" max="100" class="slider" />
                <br />
                <InputNumberBox v-model="opacity" :step="1"></InputNumberBox>
            </div>
            <br>
            <div>
                Blur:
                <input v-model="blur" type="range"  min="0" max="10" class="slider" />
                <br />
                <InputNumberBox v-model="blur" :step="0.1"></InputNumberBox>
            </div>
            <br>
            <div>
                <InputButton text="Reset Filters" color="Red" @click="reset_filters"></InputButton>
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
    margin-right: 25%;
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
}

.big {
    box-sizing: border-box;
    width: 100%;
    height: 20em;
    margin: 0px 0px;
}


</style>

