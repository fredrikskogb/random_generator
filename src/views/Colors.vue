<template>
  <div>
    <div class="child-color-container">
      <ColorBlock class="color-block"
                   :color="generatedColor"></ColorBlock>
      <ColorBlock class="color-block"
                   v-if="displayInvertedColor"
                   :inverted="true"
                   :color="invertedColor"></ColorBlock>
    </div>
    <div class="color-options">
      <div class="color-option">
        <label for="complementary-color">Complementary color</label>
        <input id="complementary-color"
               type="checkbox"
               @click="displayInvertedColor = !displayInvertedColor">
      </div>
      <button class="generator-button color-option"
              @click="randomColor">Generate</button>
    </div>
  </div>
</template>

<script lang="ts">

  import Vue from 'vue'
  import ColorBlock from '@/components/ColorBlock.vue'

  export default Vue.extend ({
    name: 'Colors',
    data() {
      return {
        red: 0,
        green: 0,
        blue: 0,
        generatedColor: '',
        invertedColor: '',
        displayInvertedColor: false
      }
    },
    components: {
      ColorBlock
    },
    created() {
      this.randomColor();
    },
    methods: {
      randomColor(): void {
        this.red = this.randomNumber();
        this.green = this.randomNumber();
        this.blue = this.randomNumber();
        this.generatedColor = `rgb(${this.red},${this.green},${this.blue})`;
        this.invertedColor = this.invertColor();
      },
      randomNumber(): number {
        return (Math.random() * 255 | 0) + 1;
      },
      invertColor(): string {
        return `rgb(${255 - this.red},${255 - this.green},${255 - this.blue})`;
      }
    }
  })

</script>

<style lang="less" scoped>
  .child-color-container {
    display: flex;
    justify-content: center;
    margin: 0.5em 0.5em 0 0.5em;
    .color-block {
      margin: 0.5em 0.5em 0 0.5em;
    }
  }
  .color-options {
    .color-option {
      margin: 5px;
    }
    .generator-button {
      cursor: pointer;
    }
  }

</style>