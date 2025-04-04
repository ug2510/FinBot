<template>
  <q-layout view="hHh lpR fFf">
    <q-header :class="headerClass" elevated>
      <q-toolbar>
        <q-btn flat round dense icon="menu" @click="toggleSidebar" />
        <q-toolbar-title>Finance AI Chatbot</q-toolbar-title>
        <q-space />
        <q-toggle v-model="darkMode" icon="brightness_4" />
      </q-toolbar>
    </q-header>

    <q-drawer v-model="leftDrawerOpen" side="left" overlay bordered :class="drawerClass">
      <sideBar :darkMode="darkMode" />
    </q-drawer>

    <q-page-container :class="pageClass">
      <chat-interface :darkMode="darkMode" />
    </q-page-container>
  </q-layout>
</template>

<script>
import sideBar from '../components/sideBar.vue'
import chatInterface from '../components/chatInterface.vue'

export default {
  components: {
    sideBar,
    chatInterface,
  },
  data() {
    return {
      leftDrawerOpen: false,
      darkMode: this.$q.dark.isActive,
    }
  },
  computed: {
    headerClass() {
      return this.darkMode ? 'bg-dark text-white' : 'bg-white text-dark'
    },
    drawerClass() {
      return this.darkMode ? 'bg-grey-10 text-white' : 'bg-white text-black'
    },
    pageClass() {
      return this.darkMode ? 'bg-black text-white' : 'bg-grey-1 text-black'
    },
  },
  watch: {
    darkMode(newValue) {
      this.$q.dark.set(newValue)
    },
  },
  methods: {
    toggleSidebar() {
      this.leftDrawerOpen = !this.leftDrawerOpen
    },
  },
}
</script>

<style>
.q-header {
  z-index: 10000 !important; 
  position: relative; 
}
</style>
