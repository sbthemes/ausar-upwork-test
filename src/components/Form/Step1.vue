<script setup>
    import { reactive } from 'vue';
    import { useVuelidate } from '@vuelidate/core';
    import { required } from '@vuelidate/validators';

    const emit = defineEmits(['submit']);

    const params = reactive({
        firstName: '',
        lastName: '',
    });

    const rules = {
        firstName: { required },
        lastName: { required },
    };

    const v$ = useVuelidate(rules, params);

    const submitForm = async () => {
        const isFormCorrect = await v$.value.$validate();
        if (!isFormCorrect) {
            return;
        }

        emit('submit', params);
    };
</script>

<template>
    <div>
        <h1 class="text-xl font-bold text-center">Step 1</h1>
        <form class="bg-gray-50 rounded p-4 mt-4 space-y-4" @submit.prevent="submitForm()">
            <div>
                <label>First name*</label>
                <div class="mt-1">
                    <input v-model="params.firstName" type="text" :class="{ 'border-red-600': v$.firstName.$errors.length }" class="w-full border border-gray-300 rounded p-2" @blur="v$.firstName.$touch" />
                </div>
                <div v-if="v$.firstName.$error" class="text-red-600 text-sm mt-0.5">First name is required.</div>
            </div>

            <div :class="{ error: v$.lastName.$errors.length }">
                <label>Last name*</label>
                <div class="mt-1">
                    <input v-model="params.lastName" type="text" :class="{ 'border-red-600': v$.lastName.$errors.length }" class="w-full border border-gray-300 rounded p-2" @blur="v$.lastName.$touch" />
                </div>
                <div v-if="v$.lastName.$error" class="text-red-600 text-sm mt-0.5">Last name is required.</div>
            </div>

            <div class="flex items-center">
                <button type="submit" class="btn ml-auto">Next</button>
            </div>
        </form>
    </div>
</template>
