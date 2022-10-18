<script setup>
import { useForm } from "@inertiajs/inertia-vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import InputForm from "@/Components/Form/InputForm.vue";
import ErrorForm from "@/Components/Form/ErrorForm.vue";
import CreateEditLayout from "@/Layouts/Form/CreateEditLayout.vue";

const form = useForm({
    name: "",
});

const submit = () => {
    form.post(route("categories.store"));
};
</script>

<template>
    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Category Create
            </h2>
        </template>
        <CreateEditLayout>
            <template #flash :flash="$page.props.flash.message"
                >{{ $page.props.flash.message }}
            </template>
            <template #form>
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
            </template>
        </CreateEditLayout>
    </AuthenticatedLayout>
</template>
