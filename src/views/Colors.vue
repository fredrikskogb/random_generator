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
        <input id="complementary-color"
               type="checkbox"
               @click="displayInvertedColor = !displayInvertedColor">
        <label for="complementary-color">Complementary color</label>
      </div>
      <div>
        <input id="opacity"
               type="number"
               max="1"
               min="0"
               step="0.1"
               v-model="opacity"
               v-on:change="setColors">
        <label for="opacity"> Opacity</label>
      </div>
      <button class="generator-button color-option"
              @click="randomColor">Generate</button>
      <div class="lower-section">
        <p class="color-option">or enter color to invert</p>
        <div class="individual-color">
          <div class="color-option">
            <input type="number" max="255" min="0" v-model="red">
            <label> Red</label>
          </div>

          <div class="color-option">
            <input type="number" max="255" min="0" v-model="green">
            <label> Green</label>
          </div>

          <div class="color-option">
            <input type="number" max="255" min="0" v-model="blue">
            <label> Blue</label>
          </div>
        </div>
        <button class="generator-button color-option"
                @click="setColors">Set color</button>
      </div>
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
        opacity: 0,
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
        this.setColors();
      },
      randomNumber(): number {
        return (Math.random() * 255 | 0) + 1;
      },
      setColors(): void {
        if(this.opacity == 0) {
          this.generatedColor = `rgb(${this.red},${this.green},${this.blue})`;
          this.invertedColor = `rgb(${255 - this.red},${255 - this.green},${255 - this.blue})`;
        } else {
          this.generatedColor = `rgb(${this.red},${this.green},${this.blue},${this.opacity})`;
          this.invertedColor = `rgb(${255 - this.red},${255 - this.green},${255 - this.blue},${this.opacity})`;
        }
      },

    }
  })

</script>

<style lang="less" scoped>
  .child-color-container {
    display: flex;
    justify-content: center;
    margin: 0.5em 0.5em 0 0.5em;
    flex-shrink: 0;
    flex-flow: row wrap;
    .color-block {
      margin: 0.5em 0.5em 0 0.5em;
    }
  }
  .color-options {
    width: 300px;
    text-align: left;
    margin: 1em auto;
    #complementary-color {
      margin: 0 5px 0 0;
    }
    .color-option {
      margin: 5px 0 5px 0;
    }
    .generator-button {
      cursor: pointer;
      background-color: white;
      border-radius: 5px;
      padding: 0.5em;
      border: 1px solid black;
    }
    .lower-section {
      margin-top: 1em;
      .individual-color {
        display: flex;
        flex-direction: column;
      }
    }

  }

</style>