<template>
  <v-app>
    <v-toolbar app>
      <v-spacer></v-spacer>
      <v-btn color="red" v-on:click="eliminate">SNAP</v-btn>
      <v-spacer></v-spacer>
    </v-toolbar>

    <v-content>
      <NodeNetwork/>
    </v-content>
  </v-app>
</template>

<script>
import NodeNetwork from './components/NodeNetwork'
import * as d3 from 'd3';
export default {
  
  name: 'App',
  components: {
    NodeNetwork
  },
  data () {
    return {
      //
    }
  },
  methods: {
    eliminate() {
      d3.selectAll('.snap0')
        .transition()
        .duration(3000)
        .style('opacity', 0)
    }
  }
}
</script>
