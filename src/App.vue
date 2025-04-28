<script setup>
  import { h, ref } from "vue";h

  const nombre = 'Vue!';
  const styleColor = "color: blue";
  const cabeceras = ['Horario', 'Lunes', 'Martes', 'Miercoles', 'Jueves', 'Viernes'];

  const nombre_docente = ref("")

  const counter = ref(0);
  const e = () => {
    counter.value ++;
  }
    
</script>

<template>
  
  <h1>Reservas de Laboratorios</h1>
  
  <div></div>
  
  <div .class="box-select">
    
    <select name="Selecciona Dia">
      <option value="Lunes">Lunes</option>
      <option value="Martes">Martes</option>
      <option value="Miercoles">Miercoles</option>
      <option value="Jueves">Jueves</option>
      <option value="Viernes">Viernes</option>
    </select>

    <select name="select">
      <option value="value1">Value 1</option>
      <option value="value2" selected>Value 2</option>
      <option value="value3">Value 3</option>
    </select>

    <p>Nombre docente</p>
    <input v-model="nombre_docente" placeholder="Nombre" />
     
    <div>
      <button @click="e">Add 1</button>
      <h2>Se ha hecho clic en el botón de arriba {{ counter }} veces.</h2>
    </div>

  </div>

  <table .class="box-tabla">
    <tbody>
      <tr>
        <th
          v-for="(dia, i) in cabeceras" :key="dia">
          {{ dia }}
        </th>
      </tr>
      <tr>
        <td>08:00 - 09:30</td>
        <td>Hola!!</td>
        <td>Hola martes</td>
        <td>Hola Miercoles</td>
        <td>Hola Jueves</td>
        <td>Hola Viernes</td>
      </tr>
      <tr>
        <td>09:45 - 11:15</td>
        <td>Hola!!</td>
        <td>Hola martes</td>
        <td>Hola Miercoles</td>
        <td>Hola Jueves</td>
        <td>Hola Viernes</td>
      </tr>
      <tr>
        <td>11:30 - 13:00</td>
        <td>Hola!!</td>
        <td>Hola martes</td>
        <td>Hola Miercoles</td>
        <td>Hola Jueves</td>
        <td>Hola Viernes</td>
      </tr>
      <tr>
        <td>14:00 - 15:30</td>
        <td>Hola!!</td>
        <td>Hola martes</td>
        <td>Hola Miercoles</td>
        <td>Hola Jueves</td>
        <td>Hola Viernes</td>
      </tr>
    </tbody>
  </table>
  
</template>


<style>

h1{
  position: relative;
  top: -25px;
}

table {
  border-collapse: collapse;
  height: 100%;
  width: 100%;
}

th {
  border: 1px solid rgb(160 160 160);
  background-color: rgb(82, 148, 192);
  text-align: center;
  font-weight: 550;
}

td {
  border: 1px solid rgb(160 160 160);
  text-align: center;
}

</style>
