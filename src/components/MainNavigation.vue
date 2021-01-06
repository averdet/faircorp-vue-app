<template>
  <ul class="nav nav-tabs">
    <li class="nav-item" @click="changeNav('windows')">
      <a class="nav-link" :class="{active: isCurrentNav('windows')}" aria-current="page" href="#">Windows</a>
    </li>
    <li class="nav-item" @click="changeNav('rooms')">
      <a class="nav-link" :class="{active: isCurrentNav('rooms')}" href="#" tabindex="-1" aria-disabled="true">Rooms</a>
    </li>
  </ul>
</template>


<script>
export default {
    name: 'MainNavigation',
    data: function() {
	return {
	    currentNavItem: 'windows'
	    }
    },
    methods: {
	changeNav(item) {
	    this.currentNavItem = item;
	    this.$emit('nav-updated',item);
	},
	isCurrentNav(item) {
	    return this.currentNavItem === item;
	}
    }
}
</script>
