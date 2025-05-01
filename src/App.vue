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
    // Validar informacion
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
  
  <div .class="['contenedor-general']">
    
    <div>
      <h1>Reservas de Laboratorios</h1>
    </div>

    <div></div>

    <div .class="['contenedor-box-select']">
      
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

    <div :class="['contenedor-tabla']">
      <h2>{{ mes[mesActual] }}</h2>
      <table>
        <tbody>
          <tr>
            <th><br>Horario  <br><br></th>
            <th><br>Lunes    <br><br></th>
            <th><br>Martes   <br><br></th>
            <th><br>Miercoles<br><br></th>
            <th><br>Jueves   <br><br></th>
            <th><br>Viernes  <br><br></th>
          </tr>
          <tr>
            <td>08:00 - 09:30</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
          </tr>
          <tr>
            <td>09:45 - 11:15</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
          </tr>
          <tr>
            <td>11:30 - 13:00</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
          </tr>
          <tr>
            <td>14:00 - 15:30</td>
            <td>6B<br>Matematicas<br>Carla Nail</td>
            <td><br>Libre<br><br></td>
            <td><br>Libre<br><br></td>
            <td>6B<br>Matematicas<br>Carla Nail</td>
            <td><br>Libre<br><br></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>


<style>

h1{
  position: relative;
  top: -25px;
}

.contenedor-general{
  display: flex;

}

.encabezado{
  width: 600px;
  height: 400px;
}

table{
  table-layout: fixed;
  width: 600px;  
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
