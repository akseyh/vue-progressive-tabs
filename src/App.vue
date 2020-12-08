<template>
  <div id="app">
    <progressiveTabs
      v-model="tabIndex" 
      :tabs="tabs"/>
    <button @click="tabIndex--">GERİ</button>
    <button @click="tabIndex++">İLERİ</button>
  </div>
</template>

<script>
import progressiveTabs from './progressiveTabs'
export default {
  name: 'App',
  components: {
    progressiveTabs
  },
  data() {
    return {
      tabs: ['Tab1', 'Tab2', 'Tab3', 'Tab4'],
      tabIndex: 0
    }
  }
}
</script>
