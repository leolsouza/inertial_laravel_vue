<script setup>
import { useForm, usePage } from "@inertiajs/inertia-vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import InputForm from "@/Components/Form/InputForm.vue";
import ErrorForm from "@/Components/Form/ErrorForm.vue";

const categories = usePage().props.value.category;

const form = useForm({
    name: categories.name,
});

const submit = () => {
    form.put(route("categories.update", categories.id));
};
</script>

<template>
    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Category Edit
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
                    <div class="p-6 bg-white border-b border-gray-200">
                        <form @submit.prevent="submit">
                            <div>
                                <label for="name">Category name:</label>
                                <InputForm v-model="form.name" />
                                <ErrorForm :error="form.errors.name" />
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
