//* tiene soporte para pug 
//* Se pueden compartir script y style entre componentes
<template>
  <h1>{{ variableOtroArchvio }}</h1>
  <span>Mi primer componente en vue</span>
  <p>aprendiendo vue Desde 0 Nivel muy básico</p>
  <div>
    <p>Espero llegar a poder pintar apis</p>
    <p>
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Fuga iusto et
      odit excepturi autem quidem, modi, saepe perspiciatis nulla qui sit maxime
      veritatis, eligendi id quos nihil repudiandae totam iure?
    </p>
  </div>
</template>

<script>
export default {
  name: "MiComponente",
  fecha: "2021-07-06",
  props: {
    variableOtroArchvio: String,
    variable2OtroArchivo: Boolean,
    variable3OtroArchvio: Number,
    variable4OtroArchvio: Array,
  },
};
</script>

//* con scoped solo afecta a un componente, es decir tiene un menor alcance
<style scoped>
body {
  background: bisque;
  padding: 0px;
  box-sizing: border-box;
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  font-size: 5em;
  color: black;
}
h2 {
  color: azure;
}
p {
  padding: 2rem;
  margin: 1rem;
}
span {
  background: #42b983;
}
</style>