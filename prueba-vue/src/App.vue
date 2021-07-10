<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <!-- <HelloWorld msg="HOLA MUNDO FRONT-ENT VUE " /> -->
  <!-- <OtroNombre variableOtroArchvio="PRUEBA H1 Con variable msg" /> -->
  <h1>Tabla Usuarios</h1>
  <hr />
  <!-- v-bind:usuarios ="usuarios" forma larga -->
  <div class="container">
    <!-- llamamo al evento con @ o con v-on add-usuarios del methods del componente formularioUsuarios
    y aádimos un nuevo evento agregarUsuario 
    es decir que llamo desde el componente que quiero recibir los datos  al evento que me los devuelve 
    y le asocio otro evento donde guardo los datos 
    tiene que llamarse igual los eventos
    -->
    <!-- Se recibe el evento declarado en la tablaUser y se llama a un evento que se definira en la app -->
    <formulario-usuarios @add-usuario="agregarUsuario" />
    <tabla-user :usuarios="usuarios" @eliminar-usuario="eliminarUsuario" @actualizar-usuario="actualizarUsuario"/>
  </div>
  <!-- Mensaje para comprobar que no hay ningun usuario agregado (el array de usuario esta vacio) -->
  <!-- v-if sentencia condicional se muestra el mensaje cuando usuarios = 0 -->
  <div v-if="!usuarios.length">No se han agredado usuarios</div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
// import OtroNombre from "./components/NuevoComponente.vue";
// @ hace referencia a la carpeta src
import TablaUser from "./components/TablaUser.vue";
import FormularioUsuarios from "./components/FormularioUsuarios.vue";
export default {
  name: "App",
  components: {
    // HelloWorld,
    // OtroNombre,
    TablaUser,
    FormularioUsuarios,
  },

  // equivale a los estados en React
  // se usa para devolver datos
  // se pasan como atributos y se incluyen con la sintaxis :nombre = "datos", como si fueran atributos
  // también se puede usar con v-bind:personas="personas"

  data() {
    return {
      usuarios: [
        {
          id: 1,
          nombre: "Pepe",
          apellido: "Sanchez",
          email: "pepesanchez@hotmail.com",
          edad: 23,
        },
        {
          id: 2,
          nombre: "Juan",
          apellido: "Sanchez",
          email: "juansanchez@hotmail.com",
          edad: 22,
        },
        {
          id: 3,
          nombre: "Alonso",
          apellido: "Sanchez",
          email: "alonsosanchez@hotmail.com",
          edad: 12,
        },
        {
          id: 4,
          nombre: "Luis",
          apellido: "Sanchez",
          email: "luissanchez@hotmail.com",
          edad: 11,
        },
        {
          id: 6,
          nombre: "Marcos",
          apellido: "Perez",
          email: "marcosperez@hotmail.com",
          edad: 32,
        },
      ],
    };
  },
  methods: {
    agregarUsuario(usuario) {
      let id = 0;
      if (this.usuarios.length > 0) {
        id = this.usuarios[this.usuarios.length - 1].id + 1;
      }
      //agrego el usuario que recibo del componente del formulario al array de usuarios que declare
      // utilizo ... operador spread
      //añadimos con el operador spread las propiedades del usuario, mas el id generado
      this.usuarios = [...this.usuarios, { ...usuario, id }];
    },
    // defino el evento que recibo del componente tablaUser como lo he llamado en @eliminar-usuario
    //de los usuarios del array de data() filtrame y devuelveme todos menos el de id ?
    eliminarUsuario(id){
      // filter, reduce, map, every, some, find, include ... metodos para programacion funcional
      this.usuarios = this.usuarios.filter( usuario => usuario.id !== id);
    },
    actualizarUsuario(id, usuarioActualizado){
      //recorro el array de usuarios, y compruebo si el usuario elemento que recorro 
      //es igual al id que le paso si lo es le pongo el usuarioActualizado si no le pongo el mismo usuario 
      this.usuarios = this.usuarios.map(usuario => usuario.id==id ? usuarioActualizado : usuario);
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #29629b;
  background: whitesmoke;
  margin: 1rem 3rem;
  padding: 2rem;
}
</style>
