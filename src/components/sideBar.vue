<template>
  <q-drawer side="left" overlay bordered v-model="drawer" :class="drawerClass" elevated >
    <q-list bordered separator>
      <q-item clickable v-ripple to="/">
        <q-item-section avatar>
          <q-icon name="home" />
        </q-item-section>
        <q-item-section>
          <q-item-label>Home</q-item-label>
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple to="/profile">
        <q-item-section avatar>
          <q-icon name="account_circle" />
        </q-item-section>
        <q-item-section>
          <q-item-label>Profile</q-item-label>
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple to="/settings">
        <q-item-section avatar>
          <q-icon name="settings" />
        </q-item-section>
        <q-item-section>
          <q-item-label>Settings</q-item-label>
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple to="/help">
        <q-item-section avatar>
          <q-icon name="help" />
        </q-item-section>
        <q-item-section>
          <q-item-label>Help</q-item-label>
        </q-item-section>
      </q-item>

      <q-separator />

      <q-item clickable v-ripple @click="logout">
        <q-item-section avatar>
          <q-icon name="logout" />
        </q-item-section>
        <q-item-section>
          <q-item-label>Logout</q-item-label>
        </q-item-section>
      </q-item>
    </q-list>
  </q-drawer>
</template>

<script>
export default {
  props: {
    darkMode: Boolean,
  },
  data() {
    return {
      drawer: true,
    }
  },
  computed: {
    drawerClass() {
      return this.darkMode ? 'bg-grey-10 text-white' : 'bg-white text-black'
    },
  },
  methods: {
    logout() {
      console.log('Logout clicked')
    },
  },
}
</script>
