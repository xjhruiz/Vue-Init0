<template>
  <!-- Tiene soporte para pug -->
  <div id="container containerUser">
    <table id="tablaUser" class="table">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Apellido</th>
          <th>Email</th>
          <th>Edad</th>
        </tr>
      </thead>
      <tbody>
        <!-- DINAMICO CON UN BUCLE -->
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <!--  con v-if se comprueba si las propiedades de editando es igual al id del usuario que se pulso -->
          <!-- si lo es se muestra el input para editar su valor -->
          <td v-if="editando === usuario.id">
            <input type="text" class="form-control" name=""  id=""
              v-model="usuario.nombre"/>
          </td>
          <!-- De no ser asi nos muestra el valor -->
          <td v-else>
            {{ usuario.nombre }}
          </td>
          <td v-if="editando === usuario.id">
            <input type="text" name="" id="" class="form-control" 
            v-model="usuario.apellido" />
          </td>
          <td v-else>
            {{ usuario.apellido }}
          </td>
          <td v-if="editando === usuario.id">
            <input type="email" name="" id="" class="form-control"  
            v-model="usuario.email"/>
          </td>
          <td v-else>
            {{ usuario.email }}</td>
          <td v-if="editando === usuario.id">
          <input type="number" name="" id="" class="form-control"
          v-model="usuario.edad"/>
          </td>
            <td v-else>
              {{ usuario.edad }}
            </td>
          <!-- standar kebab case para los nombre de los eventos -->
         <td v-if="editando === usuario.id">
           <button class="btn btn-success " @click="guardarUsuario(usuario)"> 💾 Guardar</button>
           <button class="btn btn-secondary ml-2 mt-2 " @click="cancelarEdicion(usuario)">❌ Cancelar</button>
         </td>
          <td v-else>
             <button class="btn btn-info " @click="editarUsuario(usuario)">
              ✏️ Editar
            </button>
            <button
              class="btn btn-danger ml-2"
              @click="$emit('eliminar-usuario', usuario.id)"
            >
              🗑️ Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>

  <!-- ESTATICO 
        <tr>
          <td>Nombre1</td>
          <td>Apellido2</td>
          <td>Email3</td>
        </tr>
        <tr>
          <td>Nombre1</td>
          <td>Apellido2</td>
          <td>Email3</td>
        </tr>
        <tr>
          <td>Nombre1</td>
          <td>Apellido2</td>
          <td>Email3</td>
        </tr> 
  -->
</template>

<script>
export default {
  name: "tabla-user",
  //recibe todas las propiedades que va a recibir el componente como si fuera un array asociativo
  props: {
    // tambien se puede agregar de esta forma props: ['usuarios']
    usuarios: Array,
  },
  data() {
    return {
      editando: null,
    };
  },
  methods: {
    editarUsuario(usuario) {
      //asigno el usuario que le paso a un nuevo objeto que va a ser el que se va a editar
      //assign copia las propiedades de un objeto y devuelve este objeto,  {} forma de crear un objeto vacio
      this.usuarioAEditar = Object.assign({}, usuario);
      // asigno el usuario que se esta editando con el id del que seleccione para poder recuperar sus datos
      this.editando = usuario.id;
    },
    guardarUsuario(usuario){
      if(!usuario.nombre.length || !usuario.apellido.length || !usuario.email.length || usuario.edad<1){
        return;
      }
      //con $emit puedo enviar eventos entre componente y datos a la app.js
      this.$emit('actualizar-usuario', usuario.id, usuario);
      this.editando = null;
    },
    cancelarEdicion(usuario){
      //dejo el usuario que estaba editando como estaba antes
      //recupero el valor del usuario que estaba editando
      Object.assign(usuario, this.usuarioAEditar);
      this.editando = null;
    }
  },
};
</script>

<style scoped>
.containerUser {
  background: grey;
  margin: 0 auto;
  padding: 1rem;
  height: 30%;
}
</style>