<script setup lang="ts">
import { FullscreenModal, globalModal } from '#/modal';
import NotFound from '#/common/NotFound.vue';
import PageHome from '@/pages/PageHome.vue';
import PageHackathon from '@/pages/PageHackathon.vue';
import PageContest from '@/pages/PageContest.vue';
import PageAccount from './pages/PageAccount.vue';
import PageUserView from '#/common-pages/PageUserView.vue';
import PageLogin from '#/common-pages/PageLogin.vue';
import PageRecovery from './pages/PageRecovery.vue';
import PageTest from '@/pages/PageTest.vue';
import PageTools from './pages/PageTools.vue';
import SuperSecretFeature from '@/components/SuperSecretFeature.vue';
import SuperSecretCarrier from '@/components/SuperSecretCarrier.vue';
import { useConnectionEnforcer } from '#/scripts/ConnectionEnforcer';
import { ref, watch } from 'vue';
import { useRoute } from 'vue-router';
import recaptcha from '#/scripts/recaptcha';

const modalComponent = ref<InstanceType<typeof FullscreenModal>>();

const modal = globalModal();
watch(() => modalComponent.value, () => {
    if (modalComponent.value != undefined) modal.setModal(modalComponent.value);
});

const connectionEnforcer = useConnectionEnforcer();
connectionEnforcer.init();

window.addEventListener('error', (err) => {
    modal.showModal({ title: 'An Error Occured', content: `<span style="color: red;">${err.message}<br>${err.filename} ${err.lineno}:${err.colno}</span>`, color: 'red' });
});

// hide recaptcha badge here
const route = useRoute();
watch(() => route.params, () => {
    if (route.params.page === 'login' || route.params.page === 'account') {
        recaptcha.show();
    } else {
        recaptcha.hide();
    }
});
</script>

<template name="app">
    <NotFound></NotFound>
    <PageHome></PageHome>
    <PageHackathon></PageHackathon>
    <PageContest></PageContest>
    <PageAccount></PageAccount>
    <PageUserView></PageUserView>
    <PageLogin></PageLogin>
    <PageRecovery></PageRecovery>
    <PageTest></PageTest>
    <PageTools></PageTools>
    <FullscreenModal ref="modalComponent"></FullscreenModal>
    <SuperSecretFeature></SuperSecretFeature>
    <SuperSecretCarrier></SuperSecretCarrier>
</template>