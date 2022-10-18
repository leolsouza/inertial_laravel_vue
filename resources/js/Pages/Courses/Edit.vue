<script setup>
import { useForm, usePage } from "@inertiajs/inertia-vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import InputForm from "@/Components/Form/InputForm.vue";
import ErrorForm from "@/Components/Form/ErrorForm.vue";

const courses = usePage().props.value.course;

const categories = usePage().props.value.categories;

const form = useForm({
    name: courses.name,
    duration: courses.duration,
});

const submit = () => {
    form.put(route("courses.update", courses.id));
};
</script>

<template>
    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Course Edit
            </h2>
        </template>
        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <form @submit.prevent="submit">
                            <div>
                                <label for="name">Course name: </label>
                                <InputForm v-model="form.name" />
                                <ErrorForm :error="form.errors.name" />
                            </div>

                            <div>
                                <label for="name">Course duration: </label>
                                <InputForm v-model="form.duration" />
                                <ErrorForm :error="form.errors.duration" />
                            </div>
                            <div>
                                <label for="name">Category:</label>
                                <select
                                    v-model="form.category_id"
                                    class="w-full px-4 py-2 mt-2 border rounded-md focus:outline-none focus:ring-1 focus:ring-blue-600"
                                >
                                    <option
                                        v-for="category in categories"
                                        :value="category.id"
                                        :key="category.id"
                                    >
                                        {{ category.name }}
                                    </option>
                                </select>
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
