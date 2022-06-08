<template>
      <table class="table">
        <thead class="thead-dark">
          <tr>
            <th scope="col">Pregunta</th>
            <th scope="col">Respuesta</th>
          </tr>
        </thead>
        <tbody>
            <tr v-for="(pregunta,index) in preguntas" :key="index">
            <td>{{ pregunta.numero }}</td>  
            <td>{{ pregunta.respuestas[0]}}</td>
          </tr>
        </tbody>
          <tfoot>
            <tr>
            <th scope="col"></th>
            <th></th>
          </tr>
        </tfoot>
         </table>
</template>

<script>
export default {
  name: "src-components-formulario",
  props: [],
  mounted() {},
  data() {
    return {
preguntas : [
{ numero: 1, respuestas: ["C"] },
{ numero: 2, respuestas: ["C"] },
{ numero: 3, respuestas: ["B"] }
]}
  },
  methods: {

  },
  computed: {},

};
</script>

<style scoped lang="css">
</style>
