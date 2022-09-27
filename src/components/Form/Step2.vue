<script setup>
    import { reactive } from 'vue';

    const emit = defineEmits(['submit', 'back']);

    const params = reactive({
        middleName: '',
    });

    const submitForm = async () => {
        emit('submit', params);
    };
</script>

<template>
    <div>
        <h1 class="text-xl font-bold text-center">Step 2</h1>
        <form class="bg-gray-50 rounded p-4 mt-4 space-y-4" @submit.prevent="submitForm()">
            <div>
                <label>Middle name</label>
                <div class="mt-1">
                    <input v-model="params.middleName" type="text" class="w-full border border-gray-300 rounded p-2" />
                </div>
            </div>

            <div class="flex items-center">
                <button type="button" class="hover:underline" @click="emit('back')">Back</button>
                <button type="submit" class="btn ml-auto">Next</button>
            </div>
        </form>
    </div>
</template>
