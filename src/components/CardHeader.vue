<template>
    <div class="">
        <ul class="flex justify-center">
            <li>
                <RouterLink to="/"
                    class="m-1 px-4 py-2 border-2 border-blue-600 rounded-full hover:bg-blue-600 hover:text-white hover:transition-all hover:duration-300 dark:text-white ">
                    Home</RouterLink>
                <RouterLink to="/about"
                    class="m-1 px-4 py-2 border-2 border-blue-600 rounded-full hover:bg-blue-600 hover:text-white hover:transition-all hover:duration-300 dark:text-white">
                    About</RouterLink>
                <RouterLink to="/projects"
                    class="m-1 px-4 py-2 border-2 border-blue-600 rounded-full hover:bg-blue-600 hover:text-white hover:transition-all hover:duration-300 dark:text-white">
                    Projects</RouterLink>
                    <RouterLink to="/blog"
                    class="m-1 px-4 py-2 border-2 border-blue-600 rounded-full hover:bg-blue-600 hover:text-white hover:transition-all hover:duration-300 dark:text-white">
                    Blog</RouterLink>
            </li>
        </ul>


        <div>

        </div>
    </div>
</template>
<script setup>
import router from '../router';

const route = router.currentRoute.value.path;
</script>