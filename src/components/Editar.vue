<script setup>
import { ref } from "vue";

const empleado = ref({});
</script>

<template>
    <div class="container">
        <div class="card">
            <div class="card-header text-dark">Editar Empleado</div>
            <div class="card-body">
                <form v-on:submit.prevent="actualizarRegistro">
                    <div class="form-group">
                        <label for="Nombre:"></label>
                        <input
                            type="text"
                            required
                            v-model="empleado.nombre"
                            class="form-control"
                            name="nombre"
                            id="nombre"
                            aria-describedby="helpId"
                            placeholder="Escribe tu nombre"
                        />
                        <small id="helpId" class="form-text text-muted"
                            >Nombre</small
                        >
                    </div>

                    <div class="form-group">
                        <label for="Email:"></label>
                        <input
                            type="email"
                            required
                            v-model="empleado.email"
                            class="form-control"
                            name="email"
                            id="email"
                            aria-describedby="helpId"
                            placeholder="Escribe tu email"
                        />
                        <small id="helpId" class="form-text text-muted"
                            >Email</small
                        >
                    </div>
                    <div class="btn-group" role="group" aria-label="">
                        <button type="submit" class="btn btn-success mx-1">
                            Modificar
                        </button>
                        <router-link
                            :to="{ name: 'listar' }"
                            class="btn btn-success mx-1"
                            >Cancelar</router-link
                        >
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
