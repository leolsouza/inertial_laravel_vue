<script setup>
import { useForm, Head } from "@inertiajs/inertia-vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";

const form = useForm({
    name: "",
    duration: "",
});
const submit = () => {
    form.post(route("courses.store"), {
        preserveState: true,
    });
};

const layout = () => {
    layout: AuthenticatedLayout;
};
</script>

<template>
    <Head title="Create course" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Course Create
            </h2>
        </template>
        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <form @submit.prevent="submit">
                            <div>
                                <label for="name">Course name:</label>
                                <input
                                    name="name"
                                    type="text"
                                    v-model="form.name"
                                    class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600"
                                />
                                <div
                                    class="text-sm text-red-600"
                                    v-if="form.errors.name"
                                >
                                    {{ form.errors.name }}
                                </div>
                            </div>
                            <div>
                                <label for="name">Course duration:</label>
                                <input
                                    name="name"
                                    type="text"
                                    v-model="form.duration"
                                    class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600"
                                />
                                <div
                                    class="text-sm text-red-600"
                                    v-if="form.errors.duration"
                                >
                                    {{ form.errors.duration }}
                                </div>
                            </div>
                            <div class="flex items-center mt-4">
                                <button
                                    type="submit"
                                    :disabled="form.processing"
                                    class="px-6 py-2 text-white bg-gray-900 rounded"
                                    :class="{ 'opacity-25': form.processing }"
                                >
                                    Save
                                </button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
