<template>
  <div id="main-app" class="container">
    <div class="row">
      <h4>Title</h4>
      <div class="row button-container">
        <add-appointment @add="addItem" />
      </div>
      <div class="row search-container">
        <search-appointments
          @searchRecord="searchAppointments"
          :myKey="filterKey"
          :myDir="filterDir"
        />
      </div>
      <div class="row">
        <appointment-list
          :appointments="filteredApts"
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
import SearchAppointments from "@/components/SearchAppointments";

export default {
  name: "MainApp",
  components: {
    AppointmentList,
    AddAppointment,
    SearchAppointments,
  },
  data: function () {
    return {
      title: "Appointment List",
      appointments: [],
      aptIndex: 0,
      searchTerms: "",
      filterKey: "petName",
      filterDir: "asc",
    };
  },
  computed: {
    searchedApts: function () {
      return this.appointments.filter((item) => {
        return (
          item.petName.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.petOwner.toLowerCase().match(this.searchTerms.toLowerCase()) ||
          item.aptNotes.toLowerCase().match(this.searchTerms.toLowerCase())
        );
      });
    },
    filteredApts: function () {
      return _.orderBy(
        this.searchedApts,
        (item) => {
          return item[this.filterKey].toLowerCase();
        },
        this.filterDir
      );
    },
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
    searchAppointments: function (terms) {
      this.searchTerms = terms;
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
#main-app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

.search-container {
  /* margin-bottom: 30px; */
}
</style>
