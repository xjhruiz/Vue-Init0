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
          <td>{{ usuario.nombre }}</td>
          <td>{{ usuario.apellido }}</td>
          <td>{{ usuario.email }}</td>
          <td>{{ usuario.edad }}</td>
          <td><button class="btn btn-danger">🗑️ Eliminar</button></td>
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