<script setup>
    const emit = defineEmits(['submit', 'back']);

    const props = defineProps({
        finalParams: {
            type: Object,
            required: true,
        },
    });
</script>

<template>
    <div>
        <h1 class="text-xl font-bold text-center">Thank you!</h1>
        <div class="bg-gray-50 rounded p-4 mt-4 space-y-4">
            <pre>{{ finalParams }}</pre>
        </div>
    </div>
</template>
