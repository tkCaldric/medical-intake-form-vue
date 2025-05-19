<template>
  <form @submit.prevent="handleSubmit">
    <input v-model="form.name" placeholder="Name" required />
    <input type="date" v-model="form.dob" required />
    <select v-model="form.gender" required>
      <option disabled value="">Select Gender</option>
      <option>Male</option>
      <option>Female</option>
      <option>Prefer not to say</option>
    </select>
    <input type="number" v-model.number="form.height" placeholder="Height (cm)" />
    <input type="number" v-model.number="form.weight" placeholder="Weight (kg)" />
    <p><strong>BMI:</strong> {{ bmi }} ({{ bmiClass }})</p>
    <input v-model="form.bp" placeholder="Blood Pressure" />
    <input v-model="form.hr" placeholder="Heart Rate" />
    <textarea v-model="form.history" placeholder="Medical History"></textarea>
    <input type="file" @change="onFileChange" />
    <button type="submit">Save</button>
  </form>
</template>

<script>
export default {
  props: ['addPatient'],
  data() {
    return {
      form: {
        name: '',
        dob: '',
        gender: '',
        height: null,
        weight: null,
        bp: '',
        hr: '',
        history: '',
        photo: ''
      }
    }
  },
  computed: {
    bmi() {
      if (this.form.height && this.form.weight) {
        const h = this.form.height / 100
        return (this.form.weight / (h * h)).toFixed(1)
      }
      return '–'
    },
    bmiClass() {
      const bmi = parseFloat(this.bmi)
      if (isNaN(bmi)) return ''
      if (bmi < 18.5) return 'Underweight'
      if (bmi < 25) return 'Normal'
      if (bmi < 30) return 'Overweight'
      return 'Obese'
    }
  },
  methods: {
    onFileChange(e) {
      const file = e.target.files[0]
      const reader = new FileReader()
      reader.onload = () => {
        this.form.photo = reader.result
      }
      reader.readAsDataURL(file)
    },
    handleSubmit() {
      const patient = { ...this.form, bmi: this.bmi, bmiClass: this.bmiClass }
      this.addPatient(patient)
      this.form = { name: '', dob: '', gender: '', height: null, weight: null, bp: '', hr: '', history: '', photo: '' }
    }
  }
}
</script>
