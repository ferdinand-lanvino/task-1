<template>
  <div class="container">
    <h1>Test 1</h1>

    <div class="form">
      <div class="form-group">
        <label for="shift">Shift</label>
        <select id="shift" v-model="shift" @change="generateSchedule">
          <option value="A">Shift A</option>
          <option value="B">Shift B</option>
        </select>
      </div>

      <div class="form-group">
        <label for="workingHour">Jam Bekerja</label>
        <input type="number" id="workingHour" v-model="workingHour" @change="generateSchedule" />
      </div>

      <button @click="generateSchedule">Tampilkan Jadwal Kerja</button>
    </div>
  </div>

  <div v-if="schedules.length > 0" class="container">
    <h2>Jadwal Kerja</h2>
    <div class="schedule-card" v-for="(schedule, index) in schedules" :key="index">
      <div class="schedule-item">
        {{ schedule.time.toLocaleTimeString([], { hour: '2-digit', minute: '2-digit', hour12: false }) }} | {{
          schedule.type }}
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      shift: 'A', // Default shift, Shift A
      workingHour: 8, // Default working hour, 8 hours
      schedules: [] // Array to hold generated schedules
    };
  },
  methods: {
    generateSchedule() {
      //Add validation for working hour
      if (this.workingHour > 10) {
        alert('Maksimal jam kerja adalah 10 jam')
        return
      }
      if (this.workingHour < 1) {
        alert('Minimal jam kerja adalah 1 jam')
        return
      }

      const tempSchedules = []
      //Shift A dimulai jam 6 pagi, Shift B dimulai jam 6 sore
      const startTime = new Date().setHours(this.shift == 'A' ? 6 : 18, 0, 0)
      //Terdapat jam istirahat setiap 3 jam, tampilkan jadwal kerja secara penuh
      //Jika jam kerja 3 jam berarti, ada 3 jam kerja dan 1 jam istirahat
      for (let i = 0; i < this.workingHour; i++) {
        //Jika jam kerja 3 jam berarti, ada 3 jam kerja dan 1 jam istirahat
        if (i % 3 == 0 && i != 0) {
          tempSchedules.push({
            time: new Date(startTime + i * 60 * 60 * 1000),
            type: 'Istirahat'
          })
        }
        tempSchedules.push({
          time: new Date(startTime + i * 60 * 60 * 1000),
          type: this.shift == 'A' ? 'Kerja' : 'Kerja'
        })
      }
      //Tampilkan jadwal kerja secara penuh
      this.schedules = tempSchedules.map((schedule) => {
        let time = new Date(schedule.time)
        return {
          time: time,
          type: schedule.type
        }
      })
    }
  }
}
</script>

<style>
@import './assets/style.css';
</style>
