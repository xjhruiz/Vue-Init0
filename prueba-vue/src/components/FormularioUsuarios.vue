<template>
  <div id="formulario-persona">
    <!-- Para el uso de escuchadores de eventos se utiliza el @ o v-on (forma larga)
      ejemplo @click o v-on:click @mouseover o v-on:mouseover 
      se debe de usar e.preventDefault() para que no se refresque la pagina 
      vue cuenta con prevent = preventDefault()   
      y debe de apuntar a una funcion propia de nuestro componente, 
      las funciones de nuestro componente se pone en methods:
      -->
    <form @submit.prevent="enviarFormulario">
      <div class="container-fluid">
        <div class="row">
          <div class="col-md-3">
            <div class="form-group">
              <label for="">Nombre</label>
              <input
                v-model="usuario.nombre"
                type="text"
                name=""
                id=""
                class="form-control"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group">
              <label for="">Apellido</label>
              <input
                v-model="usuario.apellido"
                type="text"
                name=""
                id=""
                class="form-control"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group">
              <label for="">Email</label>
              <input
                v-model="usuario.email"
                type="email"
                name=""
                id=""
                class="form-control"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group">
              <label for="">Edad</label>
              <input
                v-model="usuario.edad"
                type="number"
                name=""
                id=""
                class="form-control"
              />
            </div>
          </div>
        </div>
        <div class="row">
          <div class="col-md-4">
            <div class="form-group">
              <button class="btn btn-primary">Añadir usuario</button>
            </div>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "formulario-usuario",
  data() {
    return {
      //variables de estado
      procesando: false,
      correcto: false,
      error: false,
      //objeto por el cual envio los datos a mi otro componente
      //y por el cual cojo referencia por el nombre del evento   @submit.prevent="enviarFormulario"
      usuario: {
        nombre: "",
        apellido: "",
        email: "",
        edad: "",
      },
    };
  },
  methods: {
    enviarFormulario() {
      //validaciones con las funciones de computed
      this.procesando = true;
      this.resetearEstados();
      if (
        !this.validarNombre ||
        !this.validarApellido ||
        !this.validarEmail ||
        !this.validarEdad
      ) {
        this.error = true;
        return;
      }

      // console.log("enviando...");
      // console.log(this);
      // $emit envia el nombre del evento que definimos
      //y los datos que deseemos al componene en el que se ha renderizado el componente actual.
      //standars escribir siempre los nombre de los eventos en kebab-case stander en cuanto a nombres
      //le paso el usuario de data(){usuario {...}} que recibo del componente formulario
      this.$emit("add-usuario", this.usuario);
      this.error = false;
      this.correcto = true;
      this.procesando = false;
    },
    resetearEstados() {
      this.correcto = false;
      this.error = false;
    },
  },
  // propiedades computadas computed properties
  // se suele poner despues de methods
  // validaciones simples para comprobar que no esten vacios estos campos
  computed: {
    validarNombre() {
      return this.usuario.nombre.length > 1;
    },
    validarApellido() {
      return this.usuario.apellido.length > 1;
    },
    validarEmail() {
      return this.usuario.email.length > 1;
    },
    validarEdad() {
      console.log(this.usuario.edad.value);
      return this.usuario.edad.value > 1;
    },
  },
};
</script>

<style scoped>
#formulario-persona {
  background: #ecdb54;
}
form {
  margin-bottom: 2rem;
  color: peru;
  font-family: Verdana, sans-serif;
}
</style>