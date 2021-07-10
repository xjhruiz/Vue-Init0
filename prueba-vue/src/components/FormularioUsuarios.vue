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
              <label for="nombre">Nombre</label>
              <!-- Referencias en Vue atributo ref -->
              <!-- Uso del foco para el tema de accesibilidad web se situe en el primer elemento (nombre) -->
              <!-- se pone ref="nombreAReferir" luego en el script poner this.$refs.nombreAReferir.focus(); -->
              <!-- @keypress para que se resetee el campo -->
              <input
                ref="nombre"
                v-model="usuario.nombre"
                type="text"
                name=""
                id="nombre"
                class="form-control"
                :class="{ 'is-invalid': procesando && validarNombre }"
                @focus="resetearEstados"
                @keypress="resetearEstados"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group">
              <label for="apellido">Apellido</label>
              <input
                v-model="usuario.apellido"
                type="text"
                name=""
                id="apellido"
                class="form-control"
                :class="{ 'is-invalid': procesando && validarApellido }"
                @focus="resetearEstados"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group">
              <label for="email">Email</label>
              <input
                v-model="usuario.email"
                type="email"
                name=""
                id="email"
                class="form-control"
                :class="{ 'is-invalid': procesando && validarEmail }"
                @focus="resetearEstados"
              />
            </div>
          </div>
          <div class="col-md-3">
            <div class="form-group">
              <label for="edad">Edad</label>
              <!-- para coger el estado (el valor del input ) se usa v-model="apuntando al objeto que quiero guardar y que  paso por el metodo data(){}" -->
              <!-- para aplicar y definir estilos usamos el atributo :class = { 'is-invalid': seguido de las propiedades a validad}-->
              <!-- con @focus="llamada a la funcion"  se aplica el evento onfocus a una funcion propia del componente-->

              <input
                v-model="usuario.edad"
                type="number"
                name=""
                id="edad"
                class="form-control"
                :class="{ 'is-invalid': procesando && validarEdad }"
                @focus="resetearEstados"
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
      <div class="container">
        <div class="row">
          <div class="col-md-12">
            <!-- Para mostrar los errores se usa la sentencia condicional v-if solo mostrará la condicion especificada si se evalua como true error y procesando-->
            <div
              v-if="error && procesando"
              class="alert alert-danger"
              role="alert"
            >
              Debes rellenar todos los campos!
            </div>
            <!-- Para mostrar los errores se usa la sentencia condicional v-if solo mostrará la condicion especificada si se evalua como true correcto-->
            <!-- Existen otras sentencias condicionales como v-else v-else-if igual a else else if de js -->
            <!-- # v-show para mostrar o ocultar un elemento si la propiedad es display : false -->
            <!-- diferencia entre v-if vs v-show -->
            <!-- # v-for recorre una coleccion de datos -->
            <!-- no es recomendable usar v-for con v-if, v-if evalua la primera condicion  -->
            <div v-if="correcto" class="alert alert-success" role="alert">
              La persona ha sido agregada correctamente!
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
        this.validarNombre ||
        this.validarApellido ||
        this.validarEmail ||
        this.validarEdad
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
      this.$refs.nombre.focus();
      this.error = false;
      this.correcto = true;
      this.procesando = false;
      this.usuario = {
        nombre: "",
        apellido: "",
        email: "",
      };
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
      return this.usuario.nombre.length < 1;
    },
    validarApellido() {
      return this.usuario.apellido.length < 1;
    },
    validarEmail() {
      return this.usuario.email.length < 1;
    },
    validarEdad() {
      console.log(this.usuario.edad);
      return this.usuario.edad < 1; 
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