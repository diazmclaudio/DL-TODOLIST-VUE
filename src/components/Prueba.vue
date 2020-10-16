<template>
     <div>
          <b-container>
               <b-row>
                    <b-col></b-col>
                    <b-col cols="10">
                         <b-alert
                              :show="dismissCountDown"
                              dismissible
                              variant="success"
                              @dismissed="dismissCountDown = 0"
                              @dismiss-count-down="countDownChanged"
                         >
                              Tarea completada
                         </b-alert>
                         <b-jumbotron header="ToDo List">
                              <template>
                                   <div>
                                        <b-form @submit.prevent="agregarTarea">
                                             <b-form-group
                                                  id="input-group-1"
                                                  label="Ingrese Tarea"
                                                  label-for="input-1"
                                                  class="texto"
                                             >
                                                  <b-form-input
                                                       id="input-1"
                                                       v-model="tarea"
                                                       type="text"
                                                       required
                                                       placeholder=""
                                                  ></b-form-input>
                                             </b-form-group>

                                             <b-button
                                                  type="submit"
                                                  variant="primary"
                                                  >Agregar</b-button
                                             >
                                        </b-form>
                                   </div>
                              </template>
                              <!-- <form @submit.prevent="agregarTarea">
                              <label for="tarea">Ingrese la Tarea: </label>
                              <input type="text" v-model="tarea" />
                              <b-button variant="primary" type="submit"
                                   >Agregar</b-button
                              >
                         </form> -->
                         </b-jumbotron>
                         <div v-if="tareas.length > 0">
                              <ul>
                                   <li
                                        v-for="(task, index) in tareas"
                                        :key="index"
                                        class="texto"
                                   >
                                       {{index +1}} - {{ task }}
                                        <b-button
                                             class="blanco"
                                             @click="eliminar(index)"
                                        >
                                             <b-icon
                                                  icon="check2-all"
                                                  scale="2"
                                                  variant="success"
                                             ></b-icon>
                                        </b-button>
                                   </li>
                              </ul>
                         </div>
                    </b-col>
                    <b-col></b-col>
               </b-row>
          </b-container>
     </div>
</template>

<script>
export default {
     name: "Prueba",
     data() {
          return {
               nombres: [],
               tarea: "",
               tareas: [],
               dismissSecs: 2,
               dismissCountDown: 0,
          };
     },
     methods: {
          mostrarData(nombre) {
               let resultado = this.nombres.find((res) => res == nombre);
               console.log(resultado);
               if (!resultado) {
                    this.nombres.push(nombre);
               }
          },
          agregarTarea() {
               this.tareas.push(this.tarea);
               this.tarea = "";
          },
          eliminar(valor) {
               this.showAlert();
               this.tareas.splice(valor, 1);
          },
          countDownChanged(dismissCountDown) {
               this.dismissCountDown = dismissCountDown;
          },
          showAlert() {
               this.dismissCountDown = this.dismissSecs;
          },
     },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.blanco {
     background-color: #fff;
     border-color: white;
}

.texto {
     font-size: 30px;
}
li {
     list-style: none;
}
</style>
