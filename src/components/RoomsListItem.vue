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
      <button type="button" class="btn btn-secondary me-2" @click="switchWindows">Switch Windows</button>
      <button type="button" class="btn btn-secondary me-2" @click="switchHeaters">Switch Heaters</button>
      <button type="button" class="btn btn-danger me-2" @click="deleteRoom">Delete room</button>
    </div>
    <div class="windows-list pt-3">
      <windows-list-item 
	v-for="window in room.windowList"
	:window="window"
	:key="window.id"
	:room="room"
	@window-updated="updateWindow"
	@window-deleted="deleteWindow"
	>
      </windows-list-item>
    </div>      
  </template>
</div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';
import WindowsListItem from './WindowsListItem';

export default {
  components: {
    WindowsListItem
  },
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
      },
      async switchWindows() {
	  let response = await axios.put(`${API_HOST}/api/rooms/${this.room.id}/switchWindows`);
	  this.$emit('room-updated', response.data);
      },
      async switchHeaters() {
	  let response = await axios.put(`${API_HOST}/api/rooms/${this.room.id}/switchHeaters`);
	  this.$emit('room-updated', response.data);
      },
      updateWindow(newWindow) {
      /* Find the place of window objectw ith the same Id in the array, and replace it */
      let index = this.windows.findIndex(window => window.id === newWindow.id);
      this.windows.splice(index, 1, newWindow);
    },
    deleteWindow(windowId) {
      let index = this.windows.findIndex(window => window.id === windowId);
      if (index > -1) {
	this.windows.splice(index, 1);
      }
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
