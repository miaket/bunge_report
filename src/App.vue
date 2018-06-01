<template>
  <v-app>
    <v-navigation-drawer
      class="nav-menu-drawer"
      :mini-variant="true"
      :clipped="clipped"
      v-model="drawer"
      height="20%"
      fixed

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
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-content>
      <v-layout>
        <v-fab-transition>
          <v-btn
            v-bind:class="{ goRight: navisopen }"
            v-on:click="navisopen = !navisopen"
            class="fabboy"
            @click.stop="drawer = !drawer"
            v-model="fab"
            fab
            fixed
            left
            relative
            small
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
      right: true,
      title: 'Bunge',
      fab: false,
      hidden: false,
      tabs: null,
      navisopen: true
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

  .nav-menu-drawer{
    position: absolute;
    top:45%
    transform: translateY(-50%);
  }
  .goRight{
    left:60px;
  }
</style>