<script setup>
const props = defineProps({ modelValue: [String, Number] });

const $emit = defineEmits();
</script>

<template>
    <input
        type="text"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600"
    />
</template>
