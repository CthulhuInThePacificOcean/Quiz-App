<template>
    <nav
        class="flex items-center justify-center space-x-6 bg-purple-300 p-1 font-nunito"
    >
        <li
            v-for="item in navigation"
            :key="item"
            class="list-none text-indigo-800"
        >
            <router-link v-if="item == 'home'" to="/" class="text-indigo-800">{{
                item.toUpperCase()
            }}</router-link>
            <router-link v-else :to="'/' + item" class="text-indigo-800">{{
                item.toUpperCase()
            }}</router-link>
        </li>
    </nav>
    <main class="font-nunito">
        <router-view />
    </main>
</template>

<script setup>
const navigation = ['home', 'about', 'login', 'signup', 'dashboard']
</script>
