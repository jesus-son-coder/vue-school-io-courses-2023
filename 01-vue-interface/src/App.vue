<template>
  <div id="main-app" class="container">
    <div class="row">
      <h4>Title</h4>
        <div class="row button-container">
          <font-awesome-icon icon="plus" class="mr-2" /> Add Appointment
          <br><br>
        </div>
        <div class="row">
          <appointment-list :appointments="appointments" @remove="removeItem" />
        </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import _ from "lodash";
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
      appointments: []
    }
  },
  methods: {
    removeItem: function(apt) {
      this.appointments = _.without(this.appointments, apt);
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

.button-container {
  align-items: center;
}

.svg-inline--fa {
  width: auto !important;
}
</style>
