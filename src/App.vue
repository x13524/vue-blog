<template>
  <div id="app">
    <router-view></router-view>
    <transition enter-active-class="animated fadeIn" leave-active-class="animated fadeOut">
      <dialog-box v-if="dialog.show"></dialog-box>
    </transition>
  </div>
</template>

<script>
import spinner from './components/share/spinner'
import DialogBox from './components/share/DialogBox'
import {mapState} from 'vuex'

export default {
    components: {
    // FireCanvas,
        spinner,
        DialogBox
    },
    computed: {
        ...mapState(['isLoading', 'dialog'])
    }
}
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  overflow: hidden;
  min-height: 100%;
  height: 100%;
  width: 100%;
}
</style>
