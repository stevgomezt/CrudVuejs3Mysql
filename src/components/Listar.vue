<script setup>
import { ref } from "vue";

const empleados = ref([]);

const consultarEmpleados = async () => {
    try {
        const respuesta = await fetch("http://localhost/empleados/");
        const datosRespuesta = await respuesta.json();
        console.log(datosRespuesta);
        empleados.value = []; // Limpia el array de empleados
        if (typeof datosRespuesta[0].success === "undefined") {
            empleados.value = datosRespuesta; // Asigna los nuevos datos a empleados
        }
    } catch (error) {
        console.error(error);
    }
};

consultarEmpleados();

const borrarEmpleado = (id) => {
    console.log(id);

    fetch(`http://localhost/empleados/?borrar=${id}`)
        .then((respuesta) => respuesta.json())
        .then((datosRespuesta) => {
            console.log(datosRespuesta);
            window.location.href = "listar";
        })
        .catch(console.log);
};
</script>

<template>
    <div class="container">
        <div class="card">
            <div class="card-header text-dark">Empleados</div>
            <div class="card-body">
                <table class="table">
                    <thead>
                        <tr>
                            <th>Id</th>
                            <th>Nombre</th>
                            <th>Correo</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="empleado in empleados" :key="empleado.id">
                            <td scope="row">{{ empleado.id }}</td>
                            <td>{{ empleado.nombre }}</td>
                            <td>{{ empleado.correo }}</td>
                            <td>
                                <div
                                    class="btn-group"
                                    role="group"
                                    aria-label=""
                                >
                                    <button
                                        type="button"
                                        class="btn btn-success mx-1"
                                    >
                                        Editar
                                    </button>
                                    <button
                                        type="button"
                                        class="btn btn-success mx-1"
                                        v-on:click="borrarEmpleado(empleado.id)"
                                    >
                                        Eliminar
                                    </button>
                                </div>
                            </td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
