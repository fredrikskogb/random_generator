<template>
  <div>
    <ColorsBlock :color="generatedColor"></ColorsBlock>
    <button class="generator-button"
            @click="randomColor">Generate</button>
  </div>
</template>

<script lang="ts">

  import Vue from 'vue'
  import ColorsBlock from '@/components/ColorsBlock.vue'

  export default Vue.extend ({
    name: 'Colors',
    data() {
      return {
        generatedColor: ''
      }
    },
    components: {
      ColorsBlock
    },
    created() {
      this.randomColor();
    },
    methods: {
      randomColor(): void {
        this.generatedColor = `rgb(${this.randomNumber()},${this.randomNumber()},${this.randomNumber()})`;
      },
      randomNumber(): number {
        return (Math.random() * 255 | 0) + 1;
      }
    }
  })

</script>

<style lang="less" scoped>
  .generator-button {
    cursor: pointer;
  }
</style>