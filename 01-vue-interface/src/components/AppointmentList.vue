<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="list-group list-group-flush">
      <div class="list-group-item d-flex align-items-start" v-for="(item, i) in appointments" v-bind:key="i">
        <button class="mr-2 btn btn-sm btn-danger"
                @click="$emit('remove', item)">
          <font-awesome-icon icon="trash" class="mr-2"/>
        </button>
        <div class="w-100 apt-group">
          <div class="d-flex justify-content-between">
            <span class="h4 text-primary">{{ item.petName }}</span>
            <span class="float-right">{{ formattedDate(item.aptDate) }}</span>
          </div>
          <div class="owner-name">
            <span class="font-weight-bold text-primary mr-1">Owner:</span>
            <span>{{ item.petOwner }}</span>
          </div>
          <div>{{ item.aptNotes }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome';
import moment from 'moment';

export default {
  name: 'AppointmentList',
  components: {
    FontAwesomeIcon,
  },
  props: ['appointments'],
  methods: {
    formattedDate: function(date) {
      return moment(new Date(date)).format('DD-MM-YYYY, HH:mm');
    },
  },
};
</script>

<style scoped>
.apt-group {
  margin-left: 7px;
}
</style>