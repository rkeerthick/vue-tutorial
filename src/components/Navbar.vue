<script setup>
import logo from "@/assets/img/logo.png"
import { RouterLink, useRoute } from "vue-router"

const NavLinks = [
    {
        path: "/",
        title: "Home"
    },
    {
        path: "/jobs",
        title: "Jobs"
    },
    {
        path: "/jobs/add",
        title: "Add Jobs"
    }
]

const isActiveLink = (routePath) => {
    const route = useRoute();
    return routePath === route?.path
}
</script>

<template>
    <nav class="bg-green-700 border-b border-green-500">
        <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
            <div class="flex h-20 items-center justify-between">
                <div class="flex flex-1 items-center justify-center md:items-stretch md:justify-start">
                    <!-- Logo -->
                    <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
                        <img class="h-10 w-auto" :src="logo" alt="Vue Jobs" />
                        <span class="hidden md:block text-white text-2xl font-bold ml-2">Vue Jobs</span>
                    </RouterLink>
                    <div class="md:ml-auto">
                        <div class="flex space-x-2">
                            <div v-for="{ path, title } in NavLinks" :key="path">
                                <RouterLink :to="path"
                                    :class="[isActiveLink(path) ? 'bg-green-900' : 'hover:bg-gray-900 hover:text-white', 'text-white', 'rounded-md', 'px-3', 'py-2']">
                                    {{ title }}
                                </RouterLink>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>
</template>