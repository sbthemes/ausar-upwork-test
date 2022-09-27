<script setup>
    import { ref } from '@vue/reactivity';
    import Step1 from './Step1.vue';
    import Step2 from './Step2.vue';
    import Step3 from './Step3.vue';
    import ThankYou from './ThankYou.vue';

    const currentStep = ref(1);

    const finalParams = ref({
        firstName: '',
        lastName: '',
        middleName: '',
        dateOfBirth: '',
    });

    const step1Data = (data) => {
        finalParams.value.firstName = data.firstName;
        finalParams.value.lastName = data.lastName;

        currentStep.value = 2;
    };

    const step2Data = (data) => {
        finalParams.value.middleName = data.middleName;

        currentStep.value = 3;
    };

    const step3Data = (data) => {
        finalParams.value.dateOfBirth = data.dateOfBirth;
        currentStep.value = 4;
    };
</script>

<template>
    <div class="min-h-screen flex items-center justify-center">
        <div class="max-w-sm w-full mx-auto">
            <Step1 v-show="currentStep === 1" @submit="step1Data" />
            <Step2 v-show="currentStep === 2" @submit="step2Data" @back="currentStep = 1" />
            <Step3 v-show="currentStep === 3" @submit="step3Data" @back="currentStep = 2" />
            <ThankYou v-show="currentStep === 4" :final-params="finalParams" @back="clearData" />
        </div>
    </div>
</template>
