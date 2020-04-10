<template>
  <div class="colors-block-container">
    <div class="color-container"
         ref="colorsBlock">
      <p v-if="!inverted">Main color</p>
      <span class="color-text">{{this.color}}</span>
    </div>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';

  export default Vue.extend( {
    name: 'ColorsBlock',
    props: ['color', 'inverted'],
    mounted(): void {
      this.setPropsColor();
    },
    methods: {
      setPropsColor(): void {
        const colorContainer = this.$refs['colorsBlock'] as HTMLElement;
        colorContainer.style.backgroundColor = this.color;
      }
    },
    watch: {
      color: function(): void {
        this.setPropsColor();
      }
    }
  })
</script>

<style lang="less" scoped>
  .color-container {
    margin: 0 auto;
    border-radius: 50%;
    width: 200px;
    height: 200px;
    display:flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    .color-text {
      font-family: Arial;
      font-weight: bold;
      font-size: 1.2em;
      color: white;
      mix-blend-mode: difference;
    }
  }
</style>