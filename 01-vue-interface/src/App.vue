<template>
  <div id="main-app" class="container">
    <div class="row">
      <h4>Title</h4>
      <div class="row button-container">
        <add-appointment @add="addItem" />
      </div>
      <br /><br />
      <div class="row">
        <appointment-list
          :appointments="appointments"
          @remove="removeItem"
          @edit="editItem"
        />
      </div>
    </div>
  </div>
</template>

<script>
import _ from "lodash";
import axios from "axios";
import AppointmentList from "@/components/AppointmentList";
import AddAppointment from "@/components/AddAppointment";

export default {
  name: "MainApp",
  components: {
    AppointmentList,
    AddAppointment,
  },
  data: function () {
    return {
      title: "Appointment List",
      appointments: [],
      aptIndex: 0,
    };
  },
  methods: {
    removeItem: function (apt) {
      this.appointments = _.without(this.appointments, apt);
    },
    editItem: function (id, field, text) {
      const aptIndex = _.findIndex(this.appointments, {
        aptId: id,
      });
      this.appointments[aptIndex][field] = text;
    },
    addItem: function (apt) {
      apt.aptId = this.aptIndex;
      this.aptIndex++;
      this.appointments.push(apt);
    },
  },
  mounted() {
    axios.get("./data/appointments.json").then(
      (response) =>
        (this.appointments = response.data.map((item) => {
          item.aptId = this.aptIndex;
          this.aptIndex++;
          return item;
        }))
    );
  },
};
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
  margin-bottom: 30px;
}

.svg-inline--fa {
  width: auto !important;
}
</style>
