<template>
  <div id="app">
    <header>
      <div class="title">{{title}}</div>
    </header>

    <section class="main-content w-50 mx-auto">
      <main-navigation
	@nav-updated="updateNav"
	>
      </main-navigation>
      <windows-list v-if="isCurrentNav('windows')"></windows-list>
      <rooms-list v-if="isCurrentNav('rooms')"></rooms-list>
    </section>
  </div>
</template>

<script>
import MainNavigation from './components/MainNavigation.vue';
import WindowsList from './components/WindowsList.vue';
import RoomsList from './components/RoomsList.vue';

export default {
  name: 'App',
  components: {
    MainNavigation,
    WindowsList,
    RoomsList
  },
  data: function() {
    return {
	title: 'Faircorp App',
	currentNavItem: 'windows'
    }
  },
    methods: {
	updateNav(item) {
	    this.currentNavItem = item;
	},
	isCurrentNav(item) {
	    return this.currentNavItem === item;
	}
    },
    created: function() {
	document.title = this.title
    }
}
</script>

<style lang="scss" scoped>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

</style>
