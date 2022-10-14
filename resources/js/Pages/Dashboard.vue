<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head } from "@inertiajs/inertia-vue3";
import { Link } from "@inertiajs/inertia-vue3";
</script>

<template>
    <Head title="Dashboard" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Dashboard
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8"></div>
        </div>
        <div class="mb-4">
            <Link
                class="px-6 py-2 mb-2 text-green-100 bg-green-500 rounded"
                :href="route('categories.index')"
                >Categories</Link
            >
            <Link
                class="px-6 py-2 mb-2 text-green-100 bg-green-500 rounded"
                :href="route('courses.index')"
                >Courses</Link
            >
        </div>
    </AuthenticatedLayout>
</template>
