<script setup>
import { ref } from "vue";


const fechas = ref([]);  //fechas del calendario
const mesActual = ref(); //Mes actual del calendario mostrado
const ultimoDiaSemana = ref([]);  //ultimo dia (Date) de la semana mostrado en calendario

const texto = ref("Bienvenido"); //boton Enviar "texto informativo
const Laboratorio = ref();
const SeleccionaDia = ref();
const SeleccionaHorario = ref();
const docente = ref("");
const asignatura = ref("")
const curso = ref("")


//Fecha del mes
const mes = ['Enero', 'Febrero', 'Marzo', 'Abril', 'Mayo', 'Junio', 'Julio', 'Agosto', 'Septiembre', 'Octubre', 'Noviembre', 'Diciembre']


function esTextoValido(texto) {
  const regex = /^[a-zA-ZáéíóúÁÉÍÓÚñÑ0-9 ]+$/;
  return regex.test(texto);
}


function ValidaInformacion(){
  // Validar informacion
  if(Laboratorio.value == null){
    texto.value = "Selecione un Laboratorio";
    console.log("entro");
    return
  }

  if(SeleccionaDia.value == null){
    texto.value = "Selecione un Dia";
    return
  }

  if(SeleccionaHorario.value == null){
    texto.value = "Selecione un Horario";
    return
  }

  //docente
  if(docente.value == ""){
    texto.value = "Ingrese docente";
    return
  }

  if(!esTextoValido(docente.value)){
    texto.value = "Docente, valor no permitido";
    return
  }

  if(docente.value.length > 13){
    texto.value = "No mas de 13 caracteres";
    return
  }

  //Curso
  if(curso.value == ""){
    texto.value = "Ingrese curso";
    return
  }
  if(curso.value.length > 13){
    texto.value = "No mas de 13 caracteres";
    return
  }

  //Asignatura
  if(asignatura.value == ""){
    texto.value = "Ingrese asignatura";
    return
  }
  if(asignatura.value.length > 13){
    texto.value = "No mas de 13 caracteres";
    return
  }
  texto.value = "Bienvenido"

}


/*
 * Añade los dias de la semana requerida para reservar
 * Mostrados en el mes y en el selector
 *
 */
function FechaSemanal(fechaActual) {
  mesActual.value = fechaActual.getMonth();

  let diaDeLaSemana = fechaActual.getDay(); //0 domingo, 1 lunes...
  let dia = [0, 0, 0, 0, 0, 0, 0];

  //Restamos los dias
  for(let i=0; i < diaDeLaSemana; i++){
    if(i != diaDeLaSemana)
      dia[i] = (diaDeLaSemana-i)*-1;
  }

  //Sumamos los dias
  for(let i=diaDeLaSemana; i < 7; i++){
    if(i != diaDeLaSemana)
      dia[i] = diaDeLaSemana + i;
  }

  for(let i=0; i < 7; i++){
    let fechaActualTemp = new Date(fechaActual);
    fechaActualTemp.setDate(fechaActualTemp.getDate() + dia[i]);

    if(i==6)
      ultimoDiaSemana.value = new Date(fechaActualTemp);
    
    fechas.value[i] =
      fechaActualTemp.toLocaleDateString("es-CL", {
        day: "numeric", // 2-digit
        month: "short" // numeric, 2-digit, narrow, long
      });
  }
}


//docente - curso - asignatura - Laboratorio - SeleccionaDia - SeleccionaHorario
const BotonReservar = () => {
  ValidaInformacion();
}

const botonAnterior = () => {
  let fechaActualTemp = new Date(ultimoDiaSemana.value);
  fechaActualTemp.setDate(fechaActualTemp.getDate() - 7);
  FechaSemanal(fechaActualTemp);
};

const botonSiguiente = () => {
  let fechaActualTemp = new Date(ultimoDiaSemana.value);
  fechaActualTemp.setDate(fechaActualTemp.getDate() + 1);
  FechaSemanal(fechaActualTemp);
};

const fechaActual = new Date();
FechaSemanal(fechaActual);

</script>

<template>
  <h1>Reservas de Laboratorios</h1>
  <h2></h2>

  <div v-bind:class="['contenedor-general']">
    <div v-bind:class="['contenedor-box-select']">

      <section>
        <select v-model="Laboratorio">
          <option value="lab1-primerpiso">Laboratorio Primer Piso </option>
          <option value="lab2-segundopiso">Laboratorio Segundo Piso</option>
        </select>
        <p>Laboratorio a reservar</p>
      </section>

      <section>
        <select v-model="SeleccionaDia">
          <option value="Lunes">Lunes {{ fechas[1] }}</option>
          <option value="Martes">Martes {{ fechas[2] }}</option>
          <option value="Miercoles">Miercoles {{ fechas[3] }}</option>
          <option value="Jueves">Jueves {{ fechas[4] }}</option>
          <option value="Viernes">Viernes {{ fechas[5] }}</option>
        </select>
        <p>Dia a reservar</p>
      </section>

      <section>
        <select v-model="SeleccionaHorario">
          <option value="bloque1y2">08:00 - 09:30</option>
          <option value="bloque3y4">09:45 - 11:15</option>
          <option value="bloque5y6">11:30 - 13:00</option>
          <option value="bloque7y8">14:00 - 15:30</option>
        </select>
        <p>Horario a reservar</p>
      </section>

      <section>
        <input v-model="docente" placeholder="Juan P" />
        <p>Nombre docente</p>
      </section>

      <section>
        <input v-model="curso" placeholder="8C" />
        <p>Curso</p>
      </section>

      <section>
        <input v-model="asignatura" placeholder="Matematicas" />
        <p>Asignatura</p>
      </section>

      <section>
        <button v-bind:class="['boton-reservar']" @click="BotonReservar">Reservar</button>
        <p>{{ texto }}</p>
      </section>

    </div>


    <div v-bind:class="['contenedor-tabla']">
      <div v-bind:class="['contenedor-boton-Calendar']">
        <h2>{{ mes[mesActual] }}</h2>
        <button @click="botonAnterior">< Anterior</button>
        <button @click="botonSiguiente">Siguiente ></button>
        <button disabled v-bind:class="['boton-cancelar']" @click="boton">Cancelar ultima reserva</button>
      </div>
      <table>
        <tbody>
          <tr>
            <th>Horario</th>
            <th>Lunes<br>{{ fechas[1] }}</th>
            <th>Martes<br>{{ fechas[2] }}</th>
            <th>Miercoles<br>{{ fechas[3] }}</th>
            <th>Jueves<br>{{ fechas[4] }}</th>
            <th>Viernes<br>{{ fechas[5] }}</th>
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
            <td>6B<br>Matematicasss<br>Carla Nail</td>
            <td><br>Libre<br><br></td>
          </tr>
        </tbody>
      </table>

    </div>
  </div>
</template>


<style>
.contenedor-general {
  display: flex;
  flex-direction: row;
  align-content: space-evenly;
}

.contenedor-box-select {
  display: grid;
  justify-content: center;
  align-items: center;
  flex: 0 0 50%;
}

.contenedor-tabla {
  flex: 0 0 50%;
}

.boton-reservar {
  width: 210px;
  height: 30px;
}

.boton-cancelar {
  width: 150px;
  height: 30px;
  position: relative;
  left: 390px;
}

body {
  font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
  color: black;
  background: rgb(255, 255, 255);
}

h1 {
  margin-bottom: 50px;
  margin-left: 120px;
}

section {
  margin-bottom: 15px;
}

table {
  table-layout: fixed;
  width: 700px;
  height: 400px;
  border: 1px;
  border: 1px solid rgb(160 160 160);
  border-collapse: collapse;
}

th {
  background-color: rgba(82, 148, 192, 0.864);
  text-align: center;
  border: 1px solid rgb(160 160 160);
  border-collapse: collapse;
}

td {
  text-align: center;
  border: 1px solid rgb(160 160 160);
  border-collapse: collapse;
}


select {
  width: 210px;
  height: 30px;
  letter-spacing: .5px;
  font-size: x-large;
}

input {
  width: 210px;
  height: 30px;
  font-size: medium;
}

button {
  width: 80px;
  height: 30px;
}
</style>
