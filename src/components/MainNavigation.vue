<template>
  <ul class="nav nav-tabs">
    <li class="nav-item" @click="changeNav('window')">
      <a class="nav-link" :class="{active: isCurrentNav('window')}" aria-current="page" href="#">Windows</a>
    </li>
    <li class="nav-item" @click="changeNav('room')">
      <a class="nav-link" :class="{active: isCurrentNav('room')}" href="#" tabindex="-1" aria-disabled="true">Rooms</a>
    </li>
  </ul>
</template>


<script>
export default {
    name: 'MainNavigation',
    data: function() {
	return {
	    currentNavItem: 'window'
	    }
    },
    methods: {
	changeNav(item) {
	    this.currentNavItem = item;
	},
	isCurrentNav(item) {
	    return this.currentNavItem === item;
	}
    }
}
</script>
