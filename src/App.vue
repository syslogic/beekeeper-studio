<template>
<div class="style-wrapper">
    <div class="beekeeper-studio-wrapper">
      <titlebar v-if="$config.isWindows || $config.isMac"></titlebar>      
      <connection-interface v-if="!connection"></connection-interface>
      <core-interface @databaseSelected="databaseSelected" v-else :connection="connection"></core-interface>
      <auto-updater></auto-updater>
    </div>
</div>

</template>

<script>
import { ipcRenderer } from 'electron'
import Titlebar from './components/Titlebar'
import CoreInterface from './components/CoreInterface'
import ConnectionInterface from './components/ConnectionInterface'
import AutoUpdater from './components/AutoUpdater'

export default {
  name: 'app',
  components: {
    CoreInterface, ConnectionInterface, Titlebar, AutoUpdater
  },
  data() {
    return {
    }
  },
  computed: {
    connection() {
      return this.$store.state.connection
    }
  },
  mounted() {
    this.$nextTick(() => {
      ipcRenderer.send('ready')
    })
  },
  methods: {
    databaseSelected(db) {
      console.log("Do something here! (Db selected) " + db)
    },
  }
}
</script>

<style>


</style>
