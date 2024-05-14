<template>
    <div class="container">
        <router-link class="btn btn-success my-1" to="/crear"
            >Crear Nuevo Empleado</router-link
        >
        <div class="card">
            <div class="card-header">Listar Empleados</div>
            <div class="card-body">
                <table class="table">
                    <thead>
                        <tr>
                            <th>Id</th>
                            <th>Nombre</th>
                            <th>Email</th>
                            <th>Acciones</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="empleado in empleados" :key="empleado.id">
                            <td>{{ empleado.id }}</td>
                            <td>{{ empleado.nombre }}</td>
                            <td>{{ empleado.email }}</td>
                            <td>
                                <div
                                    class="btn-group"
                                    role="group"
                                    aria-label=""
                                >
                                    <router-link
                                        :to="{
                                            name: 'editar',
                                            params: { id: empleado.id },
                                        }"
                                        class="btn btn-success mr-1"
                                    >
                                        Editar
                                    </router-link>
                                    <button
                                        v-on:click="borrarEmpleado(empleado.id)"
                                        type="button"
                                        class="btn btn-success mr-1"
                                    >
                                        Borrar
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

<script>
export default {
    data() {
        return {
            empleados: [],
        };
    },

    created: function () {
        this.consultarEmpleados();
    },

    methods: {
        consultarEmpleados() {
            fetch("http://localhost/empleados/")
                .then((respuesta) => respuesta.json())
                .then((datosRespuesta) => {
                    console.log(datosRespuesta);
                    this.empleados = [];
                    if (typeof datosRespuesta[0].success === "undefined") {
                        this.empleados = datosRespuesta;
                    } else {
                        // Manejar el caso de respuesta de error
                        console.error("Error en la respuesta del servidor");
                    }
                })
                .catch(console.error);
        },

        borrarEmpleado(id) {
            console.log(id);
            fetch("http://localhost/empleados/?borrar=" + id)
                .then((respuesta) => respuesta.json())
                .then((datosRespuesta) => {
                    console.log(datosRespuesta);
                    window.location.href = "listar";
                })
                .catch(console.error);
        },
    },
};
</script>

<style scoped></style>
