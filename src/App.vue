<script setup>
  import { h, ref } from "vue";h

  const nombre = 'Vue!';

  const docente = ref("")
  const curso = ref("")
  
  //Fecha del mes
  const fecha = new Date();
  const mesActual = ref(fecha.getMonth())
  const mes = ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre']

  const texto = ref("");
  const selecBoton = () => {
    texto.value = "Reserva Realizada con Exito."
  }
  
  
  

  const nombreMes = () =>{
    mesActual.value = fecha.getMonth(); //0 Enero, 1 Febrero ... 
    
  }

  const fechaSemanal = () =>{
    const diaDeLaSemana = fechaActual.getDay(); //0 domingo, 1 lunes...
    const semana = ['Domingo', 'Lunes', 'Martes', 'Miercoles', 'Jueves', 'Viernes', 'Sabado']
    
  }

</script>

<template>
  
  <h1>Reservas de Laboratorios</h1>
  <h2>{{ mes[mesActual] }}</h2>
  
  <div .class="box-select">
    
    
    <select name="Laboratorio">
      <option value="lab1" selected>Laboratorio Primer Piso </option>
      <option value="lab2">Laboratorio Segundo Piso</option>
    </select>
    <p>Elegir Laboratorio a reservar</p>
    
    <select name="Selecciona Dia">
      <option value="Lunes" selected>Lunes</option>
      <option value="Martes">Martes</option>
      <option value="Miercoles">Miercoles</option>
      <option value="Jueves">Jueves</option>
      <option value="Viernes">Viernes</option>
    </select>
    <p>Elegir dia a reservar</p>

    <select name="Selecciona Horario">
      <option value="bloque1" selected>08:00 - 09:30</option>
      <option value="bloque2">09:45 - 11:15</option>
      <option value="bloque3">11:30 - 13:00</option>
      <option value="bloque4">14:00 - 15:30</option>
    </select>
    <p>Elegir bloque a reservar</p>
  
    <input v-model="docente" placeholder="Nombre" />
    <p>Nombre docente</p>

    <input v-model="curso" placeholder="Curso" />
    <p>Curso</p>

    <div>
      <button @click="selecBoton">Reservar</button>
      <h2>{{ texto }}</h2>
    </div>

  </div>

  <table .class="box-tabla">
    <tbody>
      <tr>
        <th>Horario</th>
        <th>Lunes</th>
        <th>Martes</th>
        <th>Miercoles</th>
        <th>Jueves</th>
        <th>Viernes</th>
      </tr>
      <tr>
        <td>08:00 - 09:30</td>
        <td>Hola Lunes</td>
        <td>Hola martes</td>
        <td>Hola Miercoles</td>
        <td>Hola Jueves</td>
        <td>Hola Viernes</td>
      </tr>
      <tr>
        <td>09:45 - 11:15</td>
        <td>Hola Lunes</td>
        <td>Hola martes</td>
        <td>Hola Miercoles</td>
        <td>Hola Jueves</td>
        <td>Hola Viernes</td>
      </tr>
      <tr>
        <td>11:30 - 13:00</td>
        <td>Hola Lunes</td>
        <td>Hola martes</td>
        <td>Hola Miercoles</td>
        <td>Hola Jueves</td>
        <td>Hola Viernes</td>
      </tr>
      <tr>
        <td>14:00 - 15:30</td>
        <td>Hola Lunes</td>
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

h2{
  position: relative;
}
</style>
