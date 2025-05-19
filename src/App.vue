<template>
  <main class="container">
    <h1>Medical Intake System</h1>
    <nav class="tabs">
      <button v-for="tab in tabs"
              :key="tab"
              :class="{ active: currentTab === tab }"
              @click="currentTab = tab">
        {{ tab }}
      </button>
    </nav>

    <component :is="currentTabComponent"
               :patients="patients"
               :addPatient="addPatient"
               :selectedPatient="selectedPatient"
               :selectPatient="selectPatient"
               :clearAll="clearAll" />
  </main>
</template>

<script>
import PatientForm from './components/PatientForm.vue'
import PatientPanel from './components/PatientPanel.vue'
import AboutTab from './components/AboutTab.vue'

export default {
  components: { PatientForm, PatientPanel, AboutTab },
  data() {
    return {
      patients: JSON.parse(localStorage.getItem('patients') || '[]'),
      selectedPatient: null,
      currentTab: 'Intake Form',
      tabs: ['Intake Form', 'Patient Panel', 'About']
    }
  },
  computed: {
    currentTabComponent() {
      return {
        'Intake Form': 'PatientForm',
        'Patient Panel': 'PatientPanel',
        'About': 'AboutTab'
      }[this.currentTab]
    }
  },
  methods: {
    addPatient(newPatient) {
      this.patients.push(newPatient)
      this.save()
    },
    selectPatient(index) {
      this.selectedPatient = this.patients[index]
    },
    clearAll() {
      if (confirm('Clear all patient data?')) {
        this.patients = []
        this.selectedPatient = null
        this.save()
      }
    },
    save() {
      localStorage.setItem('patients', JSON.stringify(this.patients))
    }
  }
}
</script>

<style>
body {
  font-family: sans-serif;
  background: #f2f2f2;
  margin: 0;
  padding: 20px;
}

.container {
  background: white;
  padding: 20px;
  max-width: 900px;
  margin: auto;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  box-sizing: border-box;
}

/* Tabs layout */
.tabs {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
}

.tabs button {
  padding: 10px 16px;
  border: none;
  background: #ccc;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
}
.tabs .active {
  background: #3498db;
  color: white;
}

/* Form grid */
form {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
  gap: 12px;
}

input, select, textarea {
  padding: 10px;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 6px;
  box-sizing: border-box;
  width: 100%;
}

textarea {
  min-height: 60px;
  resize: vertical;
}

/* Patient info card */
.patient-info {
  display: flex;
  gap: 16px;
  flex-wrap: wrap;
  background: #f8f8f8;
  padding: 16px;
  border-radius: 8px;
  margin-top: 16px;
  box-sizing: border-box;
}

.patient-info img {
  width: 100px;
  height: 100px;
  object-fit: cover;
  border-radius: 6px;
}

.patient-details {
  display: grid;
  grid-template-columns: max-content 1fr;
  gap: 6px 12px;
  flex: 1;
}

button {
  padding: 12px 20px;
  font-weight: bold;
  border: none;
  border-radius: 6px;
  background: #3498db;
  color: white;
  cursor: pointer;
}

button:hover {
  background: #2980b9;
}

.panel-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-top: 20px;
  justify-content: center;
}

/* Mobile-friendly tweak */
@media (max-width: 500px) {
  .patient-details {
    grid-template-columns: 1fr;
  }
}
</style>
