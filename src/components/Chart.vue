<template>
  <div class="chart">
    <div class="chart-title">{{ title }}</div>
    <div class="chart-content">
      <div 
        v-for="item, i in data"
        :key="i"
        :style="{backgroundColor: item.color, width: item.value*100/total + '%'}"
      ></div>   
      <svg class="chart-axis" xmlns="http://www.w3.org/2000/svg" :viewBox="viewBox">
        <defs>
          <marker id="arrowhead" markerWidth="10" markerHeight="7" 
          refX="0" refY="3.5" orient="auto" fill="#fff">
            <polygon points="0 0, 10 3.5, 0 7" />
          </marker>
        </defs>
        <line x1="0" y1="50" :x2="axisWidth" y2="50" stroke="#fff" 
        stroke-width="8" marker-end="url(#arrowhead)" stroke-dasharray="20,20" stroke-dashoffset="0" />
      </svg>             
    </div>
    <div class="chart-label">
      <div>{{ min }}</div>
      <div>{{ max }}</div>
    </div>          
  </div>
</template>

<script>
export default {
  props: ['title', 'min', 'max', 'axisWidth', 'data'],
  computed: {
    total: function() {
      let sum = 0;
      for(let item of this.data) {
        sum += item.value;
      }
      return sum;
    },
    viewBox: function() {
      return `0 0 ${this.axisWidth+100} 100`;
    }
  }
}
</script>
