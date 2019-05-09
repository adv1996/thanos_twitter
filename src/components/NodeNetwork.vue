<template>
  <v-container fill-height="true">
    <svg id='graph'/>
  </v-container>
</template>

<script>
  import * as d3 from 'd3';
  import FriendsList from '../data/twitter_friends.json'
  export default {
    data() {
      return {
        width: null,
        height: null,
      }
    },
    mounted() {
      this.initGraph()

      // todo need to create thanos fade dynamic
      // need to add sound
      // need to relocate the snap button
      // need to add thanos glove / make snap button bigger and more intimidating
      // need to show followers before and after snap
      // need to actually delete followers
      // need to add styling
    },
    methods: {
      initGraph() {
        // need to take into account margins

        this.width = this.$el.offsetWidth
        this.height = this.$el.offsetHeight

        const svg = d3.select('#graph')
          .attr('height', this.height)
          .attr('width', this.width)
        
        // simulation part
        // forceManyBody should depend on the screen size
        let simulation = d3.forceSimulation(FriendsList)
          .force('charge', d3.forceManyBody().strength(-3))
          .force('center', d3.forceCenter(this.width / 2, this.height / 2))
          .force('collision', d3.forceCollide().radius(10))
          .on('tick', ticked)
        
        simulation.tick(300)
        
        function ticked() {
          let u = d3.select('#graph')
            .selectAll('circle')
            .data(FriendsList)
          
          u.enter()
            .append('image')
            .attr('xlink:href', (d) => {
              return d.profile_pic
            })
            .attr('class', () => {return 'snap' + Math.floor(Math.random() * 2)})
            .attr('width', 40)
            .attr('height', 40)
            .attr('x', (d) => {return d.x})
            .attr('y', (d) => {return d.y})
          u.exit().remove()
        }
      }
    }
  }
</script>

<style lang="scss" scoped>

</style>