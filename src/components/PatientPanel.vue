<template>
  <div>
    <label>Select Patient:
      <select @change="select($event.target.value)">
        <option v-for="(p, i) in patients" :key="i" :value="i">{{ p.name }}</option>
      </select>
    </label>

    <PatientCard v-if="selectedPatient" :patient="selectedPatient" />

    <div class="panel-actions">
      <button @click="admit" class="success">Admit</button>
      <button @click="discharge" class="danger">Discharge</button>
      <button @click="clearAll" class="danger">Clear All Data</button>
    </div>
  </div>
</template>

<script>
import PatientCard from './PatientCard.vue'

export default {
  props: ['patients', 'selectedPatient', 'selectPatient', 'clearAll'],
  components: { PatientCard },
  methods: {
    select(index) {
      this.selectPatient(index)
    },
    admit() {
      alert('Patient admitted')
    },
    discharge() {
      alert('Patient discharged')
    }
  }
}
</script>
