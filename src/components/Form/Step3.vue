<script setup>
    import { reactive } from '@vue/reactivity';
    import { useVuelidate } from '@vuelidate/core';
    import { required } from '@vuelidate/validators';

    const emit = defineEmits(['submit', 'back']);

    const params = reactive({
        dateOfBirth: '',
    });

    const rules = {
        dateOfBirth: { required },
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
        <h1 class="text-xl font-bold text-center">Step 3</h1>
        <form class="bg-gray-50 rounded p-4 mt-4 space-y-4" @submit.prevent="submitForm()">
            <div>
                <label>Date of birth*</label>
                <div class="mt-1">
                    <input v-model="params.dateOfBirth" type="date" :class="{ 'border-red-600': v$.dateOfBirth.$errors.length }" class="w-full border border-gray-300 rounded p-2" @blur="v$.dateOfBirth.$touch" />
                </div>
                <div v-if="v$.dateOfBirth.$error" class="text-red-600 text-sm mt-0.5">Date of birth is required.</div>
            </div>
            <div class="flex items-center">
                <button type="button" class="hover:underline" @click="emit('back')">Back</button>
                <button type="submit" class="btn ml-auto">Submit</button>
            </div>
        </form>
    </div>
</template>
