<template>
  <v-app>
    <v-navigation-drawer
      :mini-variant="miniVariant"
      :clipped="clipped"
      temporary
      v-model="drawer"
      enable-resize-watcher
      fixed
      app
    >
      <v-list>
        <v-list-tile
          value="true"
          v-for="(item, i) in items"
          :key="i"
        >
          <v-list-tile-action>
            <v-icon v-html="item.icon"></v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title"></v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      app
      :clipped-left="clipped"
    >
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <!-- <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn> -->
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-content>
      <v-layout>
        <v-fab-transition>
          <v-btn
            class="fabboy"
            @click.stop="drawer = !drawer"
            v-model="fab"
            fab
            fixed
            left
          >
          <v-icon v-html="drawer ? 'chevron_left' : 'chevron_right'"></v-icon>
        </v-btn>
      </v-fab-transition>
        <!-- <v-btn icon @click.stop="drawer = !drawer">
          <v-icon v-html="drawer ? 'chevron_left' : 'chevron_right'"></v-icon>
        </v-btn> -->
      </v-layout>
      <router-view/>
    </v-content>
    <v-footer :fixed="fixed" app>
      <span>&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [{
        icon: 'bubble_chart',
        title: 'Inspire'
      }],
      miniVariant: true,
      right: true,
      title: 'Bunge',
      fab: false,
      hidden: false,
      tabs: null
    }
  },
  computed: {
    activeFab () {
      switch (this.tabs) {
        case 'one': return { 'color': 'indigo', icon: 'share' }
        case 'two': return { 'color': 'red', icon: 'edit' }
        case 'three': return { 'color': 'green', icon: 'keyboard_arrow_up' }
        default: return {}
      }
    }
  },
  name: 'App'
}
</script>

<style lang="stylus">
  @import './stylus/main'
  .fabboy{
    top: 50%
  }
</style>