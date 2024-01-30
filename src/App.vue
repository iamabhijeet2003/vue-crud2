<template>
  <div id="app" class="container-fluid">
    
      <div class="row">
          <div class="col-md-12">
              <h1 class="text-center">Profesores</h1>
          </div>
      </div>
      <div class="row">
          <div class="col-md-12">
            <formulario-persona @add-persona="agregarPersona" />
              <tabla-personas :personas="personas" @delete-persona="eliminarPersona" @actualizar-persona="actualizarPersona" />
          </div>
      </div>

      <div>
        
        <div class="d-grid gap-1 mt-4">
           
            <router-link to="/formulario-incidencias" class="btn btn-primary">Mostrar el formulario de Incidencias</router-link>
            <div class="col-md-12 mt-5">
              <h1 class="text-center">Incidencias</h1>
          </div>
        </div>

        <router-view class="mt-4" @add-incidencia="agregarIncidencia" @add-persona="agregarPersona">
           
        </router-view>
        
        <tabla-incidencia class="text-center" :incidencias="incidencia" @delete-incidencia="eliminarIncidencia" @actualizar-incidencia="actualizarIncidencia" />
      

       
    </div>
  </div>
  </template>
  
  <script>
  
  import TablaIncidencia from '@/components/TablaIncidencias.vue' // Import the TablaIncidencia component
  import TablaPersonas from '@/components/TablaPersonas.vue'
  import FormularioPersona from '@/components/FormularioPersonas.vue'
  export default {
      name: 'app',
      components: {
          TablaPersonas,
          FormularioPersona,
          TablaIncidencia, 
      },
      data() {
          return {
              personas: [
                  {
                      id: 1,
                      nombre: 'Josep',
                      apellido: 'Magraner i Ramon',
                      dni: '2020202020',
                      email: 'josep@email.com',
                      telefono: '2982728972',
                      horasMantenimiento: "5",
                      especialidad: "Front-End",
                      fechaIngreso: "24/02/2023",
                  },
                  {
                      id: 2,
                      nombre: 'Jose Fidel',
                      apellido: 'Oltra Landete',
                      dni: '1122121121',
                      email: 'fidel@email.com',
                      telefono: '2982728972',
                      horasMantenimiento: "6",
                      especialidad: "Back-End",
                      fechaIngreso: "24/02/2012",
                  },
                  {
                      id: 3,
                      nombre: 'Guillermo',
                      apellido: 'Vidal Frasquet',
                      dni: '65465465451',
                      email: 'daenerys@email.com',
                      telefono: '2982728972',
                      horasMantenimiento: "4",
                      especialidad: "Cybersecurity",
                      fechaIngreso: "24/02/2008",
                  },
              ],
              incidencia:[
                {
                    id: 1,
                    aula: 2,
                    descripcion: "monitor roto",
                    nivelUrgencia:"medio",
                    fechaRegistro:"02/20/22",
                    estado: "solucionado"
                },
                {
                    id: 2,
                    aula: 4,
                    descripcion: "proyector no va",
                    nivelUrgencia:"urgente",
                    fechaRegistro:"02/20/22",
                    estado: "no-solucionado"
                },
              ]
          }
      },
      methods: {
          agregarPersona(persona) {
              let id= 0;
              
              if (this.personas.length > 0) {
                  id = this.personas[this.personas.length - 1].id + 1;
              }
              
              this.personas= [...this.personas, { ...persona, id}];
          },
          eliminarPersona(id) {
              this.personas = this.personas.filter(
                  persona => persona.id !== id
              );
          },
          actualizarPersona(id, personaActualizada) {
              this.personas = this.personas.map(persona =>
                  persona.id === id ? personaActualizada : persona
              )
          },
          agregarIncidencia(incidencia) {
            let id = 0;
                if (this.incidencia.length > 0) { // Change this line to use `this.incidencia` instead of `this.incidencias`
                    id = this.incidencia[this.incidencia.length - 1].id + 1;
                }
                this.incidencia = [...this.incidencia, { ...incidencia, id }]; // Change this line to use `this.incidencia` instead of `this.incidencias`
            },
            eliminarIncidencia(id) {
                this.incidencia = this.incidencia.filter(
                    incidencia => incidencia.id !== id
                );
            },
            actualizarIncidencia(incidenciaActualizada, id) {
                this.incidencia = this.incidencia.map(incidencia =>
                    incidencia.id === id ? incidenciaActualizada : incidencia
                );
            }
      }
  }
  </script>
  
  <style>
  body {
      background: #f9f9f9;
  }
  </style>