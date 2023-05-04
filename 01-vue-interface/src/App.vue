<template>
  <div id="main-app" class="container">
    <h4>Title</h4>
    <font-awesome-icon icon="plus" class="mr-2" /> Add Appointment
    <br><br>
    <appointment-list :appointments="appointments"></appointment-list>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import axios from "axios";
import AppointmentList from '@/components/AppointmentList';

export default {
  name: 'MainApp',
  components: {
    FontAwesomeIcon,
    AppointmentList
  },
  data: function() {
    return {
      title: "Appointment List",
      appointments: [
      ]
    }
  },
  mounted() {
    axios.get("./data/appointments.json")
      .then(response => (this.appointments = response.data));
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
