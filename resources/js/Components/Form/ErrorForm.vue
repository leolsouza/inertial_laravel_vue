<script setup>
const props = defineProps({ error: String });
</script>

<template>
    <div class="text-sm text-red-600" v-if="error">
        {{ error }}
    </div>
</template>
