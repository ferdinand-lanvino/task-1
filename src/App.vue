<template>
  <div class="container">
    <h1>Test 1</h1>

    <div class="form">
      <div class="form-group">
        <label for="shift">Pilih Shift</label>
        <select id="shift" v-model="shift" @change="generateSchedule">
          <option value="A">Shift A</option>
          <option value="B">Shift B</option>
        </select>
      </div>

      <div class="form-group">
        <label for="workingHour">Jam Kerja</label>
        <input type="number" id="workingHour" v-model="workingHour" @change="generateSchedule" />
      </div>

      <button @click="generateSchedule">Tampilkan Jadwal Kerja</button>
    </div>


  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      shift: 'A', // Default shift
      workingHour: 8, // Default working hour
    };
  },
  methods: {
    generateSchedule() {
      // Implement your schedule generation logic here
      //Add validation for working hour
      if (this.workingHour > 10) {
        alert('Maksimal jam kerja adalah 10 jam');
        return;
      }

      if (this.workingHour < 1) {
        alert('Minimal jam kerja adalah 1 jam');
        return;
      }
      
      console.log('Selected Shift:', this.shift);
      console.log('Working Hour:', this.workingHour);
    }
  }
}
</script>

<!-- Import styling from css -->
<style>
@import './assets/style.css';
</style>
