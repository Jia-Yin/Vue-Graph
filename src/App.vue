<template>
  <div id="app">
    <button @click="startsin">start</button>&nbsp;&nbsp;
    <button @click="stopsin">stop</button>
    <graph-line
            :width="600"
            :height="400"
            :shape="'normal'"
            :axis-min="-1.5"
            :axis-max="1.5"
            :axis-full-mode="true"
            :labels="mylabels"
            :names="names"
            :values="values">
        <note :text="'Line Chart'"></note>
        <tooltip :names="names" :position="'right'"></tooltip>
        <legends :names="names"></legends>
        <guideline :tooltip-y="true"></guideline>
    </graph-line>
  </div>
</template>

<script>

export default {
  name: 'app',  
  data() {
    return {
      names: [ 'Data' ],
      values: [
        [  ]
      ],
      mylabels: [ 0 ],
      idx: 0,
      timer: null
    }
  },
  methods: {
    startsin: function() {
      this.timer = setInterval(this.addData, 100)
    },
    stopsin: function() {
      clearInterval(this.timer)
    },
    addData: function() {
      this.values[0].push(Math.sin(2*3.14159*this.idx/20))
      this.idx++
      this.mylabels.push(this.idx)
      if (this.values[0].length > 20) {
        this.values[0].shift()
        this.mylabels.shift()
      }
    },
  },

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
