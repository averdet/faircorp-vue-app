<template>
  <div class="window border border-secondary rounded p-2 mb-2" :class="{expanded: isExpanded}">
    <div class="top-row d-flex" @click="toggleExpand">
      <div class="window-name fw-bold pe-3">Create New Window</div>

      <div class="expand-button ms-auto">
        {{ isExpanded ? '&#9660;' : '&#9658;' }}
      </div>
    </div>
    <template v-if="isExpanded">
      <hr/>
      <form>
	<table>
	  <tr>
	<td><label for="window_name">Window Name: </label></td>
	<td><input v-model="window_name" type="text" id="window_name" name="window_name"></td>
	  </tr>
	  <tr>
	<td><label for="window_status">Window Status: </label></td>
	<td><select v-model="window_status" id="window_status" name="window_status">
	  <option disabled value="">Select Window Status</option>
	  <option value="CLOSED">Closed</option>
	  <option value="OPEN">Open</option>
	  </select></td>
	  </tr>
	  <tr>
	<td><label for="window_room">Window Room: </label></td>
	<td><select v-model="window_room" id="window_room" name="window_room">
	  <option disabled value="">Select room</option>
	  <option v-for="room in rooms" v-bind:value="room">
	    {{ room.name }}
	  </option>
	  </select></td>
	</tr>
	</table>
	<button type="button" class="btn btn-primary" @click="addWindow">Create Window</button>
      </form>
    </template>
  </div>
</template>

<script>
import axios from 'axios';
import {API_HOST} from '../config';

export default {
  name: 'WindowNew',
  data: function() {
    return {
	isExpanded: false,
	window_name: '',
	window_status: 'CLOSED',
	window_room: '',
	rooms: []
    }
  },
      created: async function() {
    let response = await axios.get(`${API_HOST}/api/rooms`);
    let rooms = response.data;
	  this.rooms = rooms;
	  this.window_room = rooms[0];
  },
  methods: {
    toggleExpand() {
	this.isExpanded = !this.isExpanded;
    },
    async addWindow() {
	let newWindow = {
	    "name": this.window_name,
	    "room": this.window_room,
	    "windowStatus": this.window_status	      
	};
	let headers = {
	    "Content-Type": "application/json"
	};
	let response = await axios.post(`${API_HOST}/api/windows`, newWindow, { headers });
	this.$emit('window-added', response.data);
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

.window {
  .top-row {
    cursor: pointer;
  }
}
</style>
