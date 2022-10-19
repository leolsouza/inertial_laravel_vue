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
    categories_id: [],
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
        <CreateEditLayout :flash="$page.props.flash.message">
            <template #flash>
                {{ $page.props.flash?.message }}
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
                        <label for="name">Categories:</label>
                        <div v-for="category in categories" :key="category.id">
                            <input
                                type="checkbox"
                                :value="category.id"
                                v-model="form.categories_id"
                            />
                            <label for="name" class="ml-2">{{
                                category.name
                            }}</label>
                        </div>
                        <div
                            class="text-sm text-red-600"
                            v-if="form.errors.categories_id"
                        >
                            {{ form.errors.categories_id }}
                        </div>
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
