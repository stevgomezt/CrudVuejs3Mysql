<script setup>
import { RouterLink, RouterView } from "vue-router";
</script>

<template>
    <header>
        <nav class="navbar navbar-expand navbar-light bg-light">
            <div class="nav navbar-nav">
                <router-link class="nav-item nav-link" to="/">Home</router-link>
                <router-link class="nav-item nav-link" to="/crear"
                    >Crear</router-link
                >
                <router-link class="nav-item nav-link" to="/listar"
                    >Listar</router-link
                >
            </div>
        </nav>
    </header>

    <router-view />
</template>

<style scoped></style>
