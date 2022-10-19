<script setup>
import { Link, useForm, usePage } from "@inertiajs/inertia-vue3";
import { computed } from "vue";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import Pagination from "@/Components/Pagination.vue";
import IndexLayout from "@/Layouts/Form/IndexLayout.vue";

const courses = computed(() => usePage().props.value.courses);

const form = useForm();

function destroy(id) {
    if (confirm("Are you sure you want to Delete?")) {
        form.delete(route("courses.destroy", id));
    }
}
</script>

<template>
    <AuthenticatedLayout>
        <IndexLayout>
            <div class="mb-4">
                <Link
                    class="px-6 py-2 mb-2 text-green-100 bg-green-500 rounded"
                    :href="route('courses.create')"
                    preserve-scroll
                >
                    Courses Create
                </Link>
            </div>
            <table class="table-auto">
                <thead class="font-bold bg-gray-300 border-b-2">
                    <tr>
                        <th class="px-4 py-2">ID</th>
                        <th class="px-4 py-2">Name</th>
                        <th class="px-4 py-2">Duration</th>
                        <th class="px-4 py-2">Category</th>
                    </tr>
                </thead>
                <tbody class="text-center">
                    <tr v-for="course in courses.data" :key="course.id">
                        <td class="px-4 py-2 border-b-2">
                            {{ course.id }}
                        </td>
                        <td class="px-4 py-2 border-b-2">
                            {{ course.name }}
                        </td>
                        <td class="px-4 py-2 border-b-2">
                            {{ course.duration }}
                        </td>
                        <td
                            class="px-4 py-2 border-b-2"
                            v-for="categories in course.categories"
                            :key="categories.id"
                        >
                            {{ categories.name }}
                        </td>

                        <td class="px-4 py-2 font-extrabold border-b-2">
                            <Link
                                class="text-green-700"
                                :href="route('courses.edit', course.id)"
                            >
                                Edit
                            </Link>
                            <Link
                                @click="destroy(course.id)"
                                class="text-red-700"
                                >Delete</Link
                            >
                        </td>
                    </tr>
                </tbody>
            </table>
            <Pagination :links="courses.links" class="mt-6" />
        </IndexLayout>
    </AuthenticatedLayout>
</template>
