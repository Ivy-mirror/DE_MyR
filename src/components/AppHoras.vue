<script>
import NuevoUser from './NuevoUser.vue'
import HojaPaciente from './HojaPaciente.vue'
export default {
  name: 'AppHoras',
  data() {
    return {
      pacientes: []
    }
  },
  components: { NuevoUser, HojaPaciente },
  methods: {
    agregarPaciente(nuevoPaciente) {
      this.pacientes.push(nuevoPaciente)
    },
    removeCard(idx) {
      this.pacientes.splice(idx, 1)
    }
  }
}
</script>

<template>
  <NuevoUser @submit-form="agregarPaciente" />
  <div v-show="pacientes.length == 0">
    <p :style="{ color: 'red', textAlign: 'center' }">No hay consultas registradas</p>
  </div>
  <div class="pacientes">
    <HojaPaciente
      v-for="(paciente, idx) in pacientes"
      :key="idx"
      :paciente="paciente.paciente"
      :fecha="paciente.fecha"
      :hora="paciente.hora"
      :gravedad="paciente.gravedad"
      :motivo="paciente.motivo"
      @remove-card="removeCard(idx)"
    />
  </div>
</template>

<style scoped>
.pacientes {
  margin-top: 2.5rem;
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
</style>
