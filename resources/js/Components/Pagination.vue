<script setup>
import { Link } from "@inertiajs/inertia-vue3";

const props = defineProps({ links: Array });
</script>

<template>
    <div v-if="props.links.length > 1">
        <div class="flex flex-wrap -mb-1">
            <div v-for="(link, key) in props.links">
                <div
                    v-if="link.url === null"
                    :key="key"
                    class="mr-1 mb-1 px-4 py-3 text-sm leading-4 text-gray-400 border rounded"
                    v-html="link.label"
                />
                <Link
                    v-else
                    class="mr-1 mb-1 px-4 py-3 text-sm leading-4 border rounded hover:bg-white focus:border-green-500 focus:text-green-500"
                    :class="{ 'bg-green-400': link.active }"
                    :href="link.url"
                    v-html="link.label"
                />
            </div>
        </div>
        <div></div>
    </div>
</template>
