<script setup>
import { Link, useForm, usePage } from "@inertiajs/inertia-vue3";
import { computed } from "vue";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import IndexLayout from "@/Layouts/Form/IndexLayout.vue";

const categories = computed(() => usePage().props.value.categories);

const form = useForm();

function destroy(id) {
    if (confirm("Are you sure you want to Delete?")) {
        form.delete(route("categories.destroy", id));
    }
}
</script>

<template>
    <AuthenticatedLayout>
        <IndexLayout>
            <div class="mb-4">
                <Link
                    class="px-6 py-2 mb-2 text-green-100 bg-green-500 rounded"
                    :href="route('categories.create')"
                >
                    Category Create
                </Link>
            </div>
            <table class="table-auto">
                <thead class="font-bold bg-gray-300 border-b-2">
                    <td class="px-4 py-2">ID</td>
                    <td class="px-4 py-2">Name</td>
                </thead>
                <tbody>
                    <tr v-for="category in categories" :key="category.id">
                        <td class="px-4 py-2">{{ category.id }}</td>
                        <td class="px-4 py-2">{{ category.name }}</td>

                        <td class="px-4 py-2 font-extrabold">
                            <Link
                                class="text-green-700"
                                :href="route('categories.edit', category.id)"
                            >
                                Edit
                            </Link>
                            <Link
                                @click="destroy(category.id)"
                                class="text-red-700"
                                >Delete</Link
                            >
                        </td>
                    </tr>
                </tbody>
            </table>
        </IndexLayout>
    </AuthenticatedLayout>
</template>
