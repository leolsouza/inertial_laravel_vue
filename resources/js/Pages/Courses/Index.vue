<script setup>
import { Link, useForm, usePage } from "@inertiajs/inertia-vue3";
import { computed } from "vue";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";

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
        <div class="overflow-hidden bg-white shadow-sm sm:rounded-lg">
            <div class="p-6 bg-white border-b border-gray-200">
                <div class="p-6 bg-white border-b border-gray-200">
                    <div class="mb-4">
                        <Link
                            class="px-6 py-2 mb-2 text-green-100 bg-green-500 rounded"
                            :href="route('courses.create')"
                        >
                            Courses Create
                        </Link>
                    </div>
                    <table>
                        <thead class="font-bold bg-gray-300 border-b-2">
                            <td class="px-4 py-2">ID</td>
                            <td class="px-4 py-2">Name</td>
                            <td class="px-4 py-2">Duration</td>
                        </thead>
                        <tbody>
                            <tr v-for="course in courses" :key="course.id">
                                <td class="px-4 py-2">{{ course.id }}</td>
                                <td class="px-4 py-2">{{ course.name }}</td>
                                <td class="px-4 py-2">
                                    {{ course.duration }}
                                </td>

                                <td class="px-4 py-2 font-extrabold">
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
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
