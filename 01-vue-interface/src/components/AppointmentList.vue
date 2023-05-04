<template>
  <div class="col-12 col-md-10 col-lg-7">
    <div class="list-group list-group-flush">
      <div
        v-for="item in appointments"
        :key="item.aptIndex"
        class="list-group-item d-flex align-items-start"
      >
        <button
          class="mr-2 btn btn-sm btn-danger"
          @click="$emit('remove', item)"
        >
          <font-awesome-icon class="mr-2" icon="trash" />
        </button>
        <div class="w-100 apt-group">
          <div class="d-flex justify-content-between">
            <span
              class="h4 text-primary"
              contenteditable="contenteditable"
              @blur="
                $emit('edit', item.aptId, 'petName', $event.target.innerText)
              "
            >
              {{ item.petName }}</span
            >
            <span class="float-right">{{ formattedDate(item.aptDate) }}</span>
          </div>
          <div class="owner-name">
            <span class="font-weight-bold text-primary mr-1">Owner: </span>
            <span
              contenteditable="contenteditable"
              @blur="
                $emit('edit', item.aptId, 'petOwner', $event.target.innerText)
              "
              >{{ item.petOwner }}</span
            >
          </div>
          <div
            contenteditable="contenteditable"
            @blur="
              $emit('edit', item.aptId, 'aptNotes', $event.target.innerText)
            "
          >
            {{ item.aptNotes }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import moment from "moment";

export default {
  name: "AppointmentList",
  components: {
    FontAwesomeIcon,
  },
  props: ["appointments"],
  methods: {
    formattedDate: function (date) {
      return moment(new Date(date)).format("DD-MM-YYYY, HH:mm");
    },
  },
};
</script>

<style scoped>
.apt-group {
  margin-left: 7px;
}
</style>
