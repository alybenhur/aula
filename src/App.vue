<script setup>
   import {ref, reactive} from 'vue'
   const asignaturas = reactive([])
    const materia = {
        id : '',
        nombre : '',
        }

    const alumnos = reactive([])
    const alumno = {
        id : '',
        nombre : '',
        apellido : '',
        edad : '',
        celular : ''
    }

   function buscar(){
        let resultado = alumnos.find(estudiante => estudiante.id == alumno.id)
        return resultado
   }
  
function buscarasignatura(){
        let resultado = asignaturas.find(asignatura => asignatura.id == materia.id)
        return resultado
   }

   function guardarasignatura(){
   if (buscarasignatura() != undefined){
     alert('La asignatura ya se encuentra registrada')
     return
   }
     asignaturas.push({...materia})
    limpiarasignatura()
     alert('Registro exitoso...')
 }  

 function limpiarasignatura(){
   materia.id = '',
   materia.nombre = ''
 }

 function guardar(){
   if (buscar() != undefined){
     alert('El alumno ya se encuentra registrado')
     return
   }
     alumnos.push({...alumno})
    limpiar()
     alert('Registro exitoso...')
 }
 function limpiar(){
   alumno.id = '',
   alumno.nombre = '',
   alumno.apellido = '',
   alumno.edad  = '',
   alumno.celular = ''
 }
</script>

<template>
  <div>
 

  <nav class=" container navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <a class="navbar-brand" href="#">Navbar</a>
   
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
       
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Alumno
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item" data-bs-toggle="modal" data-bs-target="#exampleModal">Ingresar</a></li>
            <li><a class="dropdown-item" data-bs-toggle="modal" data-bs-target="#exampleModal2">Listado alumno</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item" href="#">Something else here</a></li>
          </ul>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdown" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Asignatura
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
            <li><a class="dropdown-item" data-bs-toggle="modal" data-bs-target="#modalasignatura">Ingresar</a></li>
            <li><a class="dropdown-item" data-bs-toggle="modal" data-bs-target="#modallistadoasignatura">Listar asignaturas</a></li>
            
          </ul>
        </li>
       
      </ul>
      <form class="d-flex">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form>
    </div>
  </div>
</nav>
  
  <!--VENTAN DE REGISTRO ALUMNO !-->
  <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">REGISTRO DE ALUMNO</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
          <div class="form-floating mb-3">
            <input type="number" class="form-control" id="floatingInput" placeholder="Identificación" v-model="alumno.id">
            <label for="floatingInput">Identificacion</label>
          </div>
        <div class="form-floating mb-3">
          <input type="text" class="form-control" id="floatingPassword" placeholder="Nombre" v-model="alumno.nombre">
          <label for="floatingPassword">Nombre</label>
        </div>
         <div class="form-floating mb-3">
          <input type="text" class="form-control" id="floatingPassword" placeholder="Apellido" v-model="alumno.apellido">
          <label for="floatingPassword">Apellido</label>
        </div>
         <div class="form-floating mb-3">
          <input type="number" class="form-control" id="floatingPassword" placeholder="Edad" v-model="alumno.edad">
          <label for="floatingPassword">Edad</label>
        </div>
         <div class="form-floating mb-3">
          <input type="text" class="form-control" id="floatingPassword" placeholder="Celular" v-model="alumno.celular">
          <label for="floatingPassword">Celular</label>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" @click="guardar">Guardar</button>
      </div>
    </div>
  </div>
</div>
<!--FIN VENTAN DE REGISTRO ALUMNO !-->
<!--VENTAN LISTADO ALUMNO !-->
  <div class="modal fade" id="exampleModal2" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">LISTADO DE ALUMNOS</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <table class="tabla table table-dark table-hover">
           <thead>
             <th>IDENTIFICACION</th>
             <th>NOMBRE</th>
             <th>APELLIDO</th>
             <th>EDAD</th>
             <th>CELULAR</th>
           </thead>
           <tr v-for="data in alumnos" :key="data.id">
             <td>{{ data.id }}</td>
             <td>{{ data.nombre }}</td>
             <td>{{ data.apellido }}</td>
             <td>{{ data.edad }}</td>
             <td>{{ data.celular }}</td>
           </tr>
      </table>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" @click="guardar">Guardar</button>
      </div>
    </div>
  </div>
</div>
<!--FIN VENTAN DE REGISTRO ALUMNO !-->

  <!--VENTAN DE REGISTRO ASIGNATURA !-->
  <div class="modal fade" id="modalasignatura" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">REGISTRO DE ASIGNATURA</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
          <div class="form-floating mb-3">
            <input type="number" class="form-control" id="floatingInput" placeholder="Id Asignatura" v-model="materia.id">
            <label for="floatingInput">Id Asignatura</label>
          </div>
        <div class="form-floating mb-3">
          <input type="text" class="form-control" id="floatingPassword" placeholder="Nombre Asignatura" v-model="materia.nombre">
          <label for="floatingPassword">Nombre Asignatura</label>
        </div>
        
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" @click="guardarasignatura">Guardar</button>
      </div>
    </div>
  </div>
</div>

<!--VENTAN LISTADO Asignatura !-->
  <div class="modal fade" id="modallistadoasignatura" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel">LISTADO DE ASIGNATURAS</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        <table class="tabla table table-dark table-hover">
           <thead>
             <th>ID ASIGNATURA</th>
             <th>NOMBRE</th>
           </thead>
           <tbody>
             <tr v-for="asignatura in asignaturas" :key="asignatura.id">
               <td>{{ asignatura.id }}</td>
               <td>{{ asignatura.nombre }}</td>
             </tr>
           </tbody>
        </table>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary" @click="guardar">Guardar</button>
      </div>
    </div>
  </div>
</div>
  </div>

</template>

<style scoped>
   .titulo{
     height: 100px;
     font-weight: bold;
   }

   .tabla{
    background-color: black;
   }
</style>
