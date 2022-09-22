<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated class="glossy">
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          @click="leftDrawerOpen = !leftDrawerOpen"
          aria-label="Menu"
          icon="menu"
        />

        <q-toolbar-title>
          Quasar App
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-grey-2"
    >
      <q-list>
        <q-item-label header>Pokémon</q-item-label>

        <drawer-menu-item type="sidebar" to="/pokedex" iconName="sports_esports" name="Pokédex" />
        <drawer-menu-item type="sidebar" to="/jeu" iconName="sports_esports" name="Jeu" />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from 'vue'
import DrawerMenuItem from './components/DrawerMenuItem.vue'

export default {
  name: 'LayoutDefault',

  components: {
    DrawerMenuItem
  },

  setup () {
    return {
      leftDrawerOpen: ref(false)
    }
  }
}
</script>
