<template>
  <div class="patient-info">
    <img :src="patient.photo" v-if="patient.photo" alt="Photo" />
    <div class="patient-details">
      <strong>Name:</strong> <div>{{ patient.name }}</div>
      <strong>DOB:</strong> <div>{{ patient.dob }}</div>
      <strong>Gender:</strong> <div>{{ patient.gender }}</div>
      <strong>Height:</strong> <div>{{ patient.height }} cm</div>
      <strong>Weight:</strong> <div>{{ patient.weight }} kg</div>
      <strong>BMI:</strong> <div>{{ patient.bmi }} ({{ patient.bmiClass }})</div>
      <strong>BP:</strong> <div>{{ patient.bp }}</div>
      <strong>HR:</strong> <div>{{ patient.hr }}</div>
      <strong>History:</strong> <div>{{ patient.history || 'None' }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['patient']
}
</script>
