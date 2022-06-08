<template>
  <section class="src-components-formulario">
    <div class="jumbotron">
      <vue-form :state="formState" @submit.prevent="enviar()">
        <!-- Campo nombre -->
        <validate tag="div">
          <label for="nombre">Nombre</label>
          <input
            type="text"
            id="nombre"
            name="nombre"
            class="form-control"
            v-model.trim="formData.nombre"
            autocomplete="off"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"    
          />

          <field-messages name="nombre" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere entre {{ nombreMinLength }} y
              {{ nombreMaxLength }} caracteres
            </div>
            <div slot="no-espacios" class="alert alert-danger mt-1">
              No se permite espacios intermedios en este campo
            </div>
          </field-messages>
        </validate>
         <!-- Campo Apellido -->
        <validate tag="div">
          <!-- elemento de entrada -->
          <label for="apellido">Apellido</label>
          <input
            type="text"
            id="apellido"
            name="apellido"
            class="form-control"
            v-model.trim="formData.apellido"
            autocomplete="off"
            required
            :minlength="nombreMinLength"
            :maxlength="nombreMaxLength"
            
          />

          <!-- Mensajes de validacion -->
          <field-messages name="apellido" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="minlength" class="alert alert-danger mt-1">
              Este campo requiere entre {{ nombre}} y
              {{ nombreMaxLength }} caracteres
            </div>
          </field-messages>
        </validate>

        <validate tag="div">
          <label for="nota">Nota</label>
          <input
            type="number"
            id="nota"
            name="nota"
            class="form-control"
            v-model.trim="formData.nota"
            autocomplete="off"
            required
            :min="notaMin"
            :max="notaMax"
          />
          <field-messages name="nota" show="$dirty">
            <div slot="required" class="alert alert-danger mt-1">
              Campo requerido
            </div>
            <div slot="notaMin" class="alert alert-danger mt-1">
              La nota debe ser entre {{notaMin}} y {{notaMax}}
            </div>
          </field-messages>
        </validate>
        
        <!-- Botón de envío -->
      <button
          type="submit"
          class="btn btn-dark my-4"
          :disabled="formState.$invalid"
        >
          Enviar
        </button>
      </vue-form>

      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col">Nombre     y     apellido</th>
            <th scope="col">Nota</th>
          </tr>
        </thead>
        <tbody>
            <tr v-for="(user,index) in users" :key="index">
            <td>{{ user.nombre +
             "       " +user.nombre }}</td>
            <td v-bind:style="{ color: getColor(user.nota)}">{{ user.nota }}</td>
          </tr>
        </tbody>
          <tfoot>
            <tr>
            <th scope="col">Promedio</th>
            <th v-bind:style="{ color: getColor(getProm())}" scope="col">{{getProm()}}</th>
          </tr>
        </tfoot>
         </table>
    </div>
  </section>
</template>

<script>
export default {
  name: "src-components-formulario",
  props: [],
  mounted() {},
  data() {
    return {
      formData: this.getInicialData(),
      formState: {},
      nombreMinLength : 3,
      nombreMaxLength: 15,
      notaMin: 0,
      notaMax: 10,
      isDisabled: false,
      promedio: 0,
      users: []
    };
  },
  methods: {
    getInicialData() {
      return {
        nombre: "",
        apellido: "",
        nota: "",
      };
    },
    enviar() {
      console.log({...this.formData});
      this.users.push({...this.formData})
      this.formData = this.getInicialData(); //reset de los datos del vue-form
      this.formState._reset(); //reseet de los estados vue-form
    },
    getColor(nota) {
      let color = "red";
      if(nota>3&&nota<=6){
       color = "yellow";
      }else if(nota>6){
        color = "green"; 
      }
      return color;
    },
    getProm() {
      let prom = 0;
     this.users.map(user=>{
       prom = prom + Number(user.nota)
     })
     prom = prom / this.users.length
     if(this.users.length == 0){
       prom = 0;
     }
     return prom;
    },
  },
  computed: {},
  isDisabled:function(){
  },
};
</script>

<style scoped lang="css">
</style>
