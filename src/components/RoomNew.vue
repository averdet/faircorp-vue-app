<template>
  <div class="room border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="room-name fw-bold pe-3">Create New Room</div>

      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <form>
	<table>
	  <tr>
	<td><label for="room_name">Room Name: </label></td>
	<td><input v-model="room_name" type="text" id="room_name" name="room_name"></td>
	  </tr>
	  <tr>
	<td><label for="room_building">Room building: </label></td>
	<td><select v-model="room_building" id="room_building" name="room_building">
	  <option disabled value="">Select building</option>
	  <option v-for="building in buildings" v-bind:value="building">
	    {{ building.name }}
	  </option>
	  </select></td>
	  </tr>
	  <tr>
	<td><label for="room_current_temperature">Room Current Temperature: </label></td>
	<td><input v-model="room_current_temperature" type="text" id="room_current_temperature" name="room_current_temperature"></td>
	  </tr>
	  <tr>
	<td><label for="room_target_temperature">Room Target Temperature: </label></td>
	<td><input v-model="room_target_temperature" type="text" id="room_target_temperature" name="room_target_temperature"></td>
	  </tr>
	  <tr>
	<td><label for="room_floor">Room Floor: </label></td>
	<td><input v-model="room_floor" type="text" id="room_floor" name="room_floor"></td>
	  </tr>

	</table>
	<button type="button" class="btn btn-primary" @click="addRoom">Create Room</button>
      </form>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';

export default {
  name: 'RoomNew',
  data: function() {
    return {
	isExpanded: false,
	room_name: '',
	room_building: '',
	room_current_temperature: '',
	room_target_temperature: '',
	room_floor: '',
	buildings: []
    }
  },
      created: async function() {
    let response = await axios.get(`${API_HOST}/api/buildings`);
    let buildings = response.data;
	  this.buildings = buildings;
	  this.room_building = buildings[0];
  },
  methods: {
    toggleExpand() {
	this.isExpanded = !this.isExpanded;
    },
    async addRoom() {
	let newRoom = {
	    "name": this.room_name,
	    "building": this.room_building,
	    "currentTemperature": this.room_current_temperature,
	    "targetTemperature": this.room_target_temperature,
	    "floor": this.room_floor
	};
	let headers = {
	    "Content-Type": "application/json"
	};
	let response = await axios.post(`${API_HOST}/api/rooms`, newRoom, { headers });
	this.$emit('room-added', response.data);
    }
  }
}
</script>

<style lang="scss" scoped>

.open-status {
  .icon {
    position: relative;
  }

  &.open {
    color: #198754;
    .icon {
      font-size: 12px;
      top: -3px;
    }
  }

  &.closed {
    color: #dc3545;
  }
}

.room {
  .top-row {
    cursor: pointer;
  }
}
</style>
