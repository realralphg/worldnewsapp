<template>
  <div id="app">
    <SourceSelection @sourceChanged="sourceChanged"/>
    <NewsList :source="source"/>
    <footer> <small>Ralph of Greysoft</small></footer>
  </div>
</template>

<script>
import NewsList from './Components/NewsList'
import SourceSelection from './Components/SourceSelection'

export default {
  name: 'app',
  components: {
    NewsList,
    SourceSelection
  },

  data () {
    return {
      source: ''
    }
  },

  methods: {
    //sourceChanged Event emitted from sourceSelection updates this.source 
    sourceChanged(source){
      this.source = source
    }
  }
}
</script>

<style>
#app {
  font-family:   sans-serif, Helvetica, Arial;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

footer {
  position: fixed;
  left: 0;
  bottom: 0;
  width: 100%;
  background-color: rgb(31, 30, 30);
  color: grey;
  text-align: center;
}

</style>
