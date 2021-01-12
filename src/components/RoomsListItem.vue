<template>
  <div class="room border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="room-name fw-bold pe-3">{{room.name}}</div>
      <div  class="room-name text-muted pe-3">{{room.building.name}}</div>
      <div  class="room-name text-muted pe-3">Floor : {{room.floor}}</div>
      <div  v-if="room.currentTemperature != null" class="room-name text-muted pe-3">Current Temperature : {{room.currentTemperature}}</div>
      <div  v-if="room.targetTemperature != null" class="room-name text-muted pe-3">Target Temperature : {{room.targetTemperature}}</div>

      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <div class="details d-flex">
        <button type="button" class="btn btn-danger " @click="deleteRoom">Delete room</button>
      </div>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';

export default {
  name: 'RoomsListItem',
  props: ['room'],
  data: function() {
    return {
      isExpanded: false
    }
  }, 
  methods: {
    toggleExpand() {
      this.isExpanded = !this.isExpanded;
    },
    async deleteRoom() {
      let response = await axios.delete(`${API_HOST}/api/rooms/${this.room.id}`);
      this.$emit('room-deleted', this.room.id);
    }
  }
}
</script>

<style lang="scss" scoped>

.room {
  .top-row {
    cursor: pointer;
  }
}
</style>
