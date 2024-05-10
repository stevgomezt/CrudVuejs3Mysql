<script setup>
import { ref } from "vue";

const empleado = ref({});

const agregarRegistro = () => {
    console.log(empleado.value);

    const datosEnviar = {
        nombre: empleado.value.nombre,
        email: empleado.value.email,
    };

    fetch("http://localhost/empleados/?insertar=1", {
        method: "POST",
        body: JSON.stringify(datosEnviar),
    })
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
            console.log(datosRespuesta);
            window.location.href = "listar";
        });
};
</script>

<template>
    <div class="container">
        <div class="card">
            <div class="card-header text-dark">Agregar Nuevo Empleado</div>
            <div class="card-body">
                <form v-on:submit.prevent="agregarRegistro">
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
                            Agregar
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
