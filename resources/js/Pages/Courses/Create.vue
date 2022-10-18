<script setup>
import { useForm, Head, usePage } from "@inertiajs/inertia-vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { computed } from "vue";
import InputForm from "@/Components/Form/InputForm.vue";
import ErrorForm from "@/Components/Form/ErrorForm.vue";
import CreateEditLayout from "../../Layouts/Form/CreateEditLayout.vue";

const form = useForm("Courses/Create", {
    name: "",
    duration: "",
    category_id: "",
});
const submit = () => {
    form.post(route("courses.store"), { onSuccess: () => form.reset() });
};

const categories = computed(() => usePage().props.value.categories);
</script>

<template>
    <Head title="Create course" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Course Create
            </h2>
        </template>
        <CreateEditLayout>
            <template #flash :flash="$page.props.flash.message">
                {{ $page.props.flash.message }}
            </template>
            <template #form>
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
                        <ErrorForm :error="form.errors.category_id" />
                    </div>
                    <div v-if="form.isDirty" class="flex items-center mt-4">
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
            </template>
        </CreateEditLayout>
    </AuthenticatedLayout>
</template>
