<script>

export default {
    data() {
        return {
            empleado: {},
        };
    },

    methods: {
        agregarRegistro() {
            console.log(this.empleado);

            var datosEnviar = {
                nombre: this.empleado.nombre,
                email: this.empleado.email,
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
        },
    },
};
</script>

<template>
    <div class="container">
        <div class="card">
            <div class="card-header">Crear Empleados</div>
            <div class="card-body">
                <form v-on:submit.prevent="agregarRegistro">
                    <div class="form-group">
                        <label for="nombre">Nombre:</label>
                        <input
                            type="text"
                            v-model="empleado.nombre"
                            class="form-control"
                            name="nombre"
                            id="nombre"
                            aria-describedby="helpId"
                            placeholder="Escriba su Nombre"
                            required
                        />
                        <small id="helpId" class="form-text text-muted"
                            >Nombre</small
                        >
                    </div>
                    <div class="form-group">
                        <label for="email">Email:</label>
                        <input
                            type="email"
                            v-model="empleado.email"
                            class="form-control"
                            name="email"
                            id="email"
                            aria-describedby="helpId"
                            placeholder="Escriba su email"
                            required
                        />
                        <small id="helpId" class="form-text text-muted"
                            >email</small
                        >
                    </div>
                    <div class="btn-group" role="group" aria-label="">
                        <button type="submit" class="btn btn-primary mr-1">
                            Agregar
                        </button>
                        <router-link to="/listar" class="btn btn-primary mr-1"
                            >Cancelar</router-link
                        >
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>

<style scoped></style>
