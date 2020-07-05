<template>
  <div>
    <div class="generate-colors-container">
      <GenerateColors class="generate-colors"
                      :color="generatedColor"></GenerateColors>
      <GenerateColors class="generate-colors"
                      v-if="displayInvertedColor"
                      :inverted="true"
                      :color="invertedColor"></GenerateColors>
    </div>
    <div class="color-options">
      <div class=upper-section>
        <div class="color-option">
        <input id="complementary-color"
               type="checkbox"
               @click="displayInvertedColor = !displayInvertedColor">
        <label for="complementary-color">Complementary color</label>
        </div>
        <div class="color-option">
          <input id="warm-color"
                type="checkbox"
                v-model="warmColor" 
                :disabled="coldColor">
          <label for="warm-color">Warm color</label>
        </div>
        <div class="color-option">
          <input id="cold-color"
                type="checkbox"
                v-model="coldColor"
                :disabled="warmColor">
          <label for="cold-color">Cold color</label>
        </div>
        <div class="color-option">
          <input id="opacity"
                type="number"
                max="0.9"
                min="0"
                step="0.1"
                v-model="opacity"
                v-on:change="setColors">
          <label for="opacity"> Opacity</label>
        </div>
        <button class="generator-button color-option"
                @click="randomColor">Generate</button>
      </div>
      
      <div class="lower-section">
        <p class="color-option">or enter color to invert</p>
        <div class="individual-color">
          <div class="color-option">
            <input type="number"
                   max="255"
                   min="0"
                   step="1"
                   v-model="red">
            <label> Red</label>
          </div>

          <div class="color-option">
            <input type="number"
                   max="255"
                   min="0"
                   step="1"
                   v-model="green">
            <label> Green</label>
          </div>

          <div class="color-option">
            <input type="number"
                   max="255"
                   min="0"
                   step="1"
                   v-model="blue">
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
  import GenerateColors from '@/components/GenerateColors.vue'

  export default Vue.extend ({
    name: 'Colors',
    data() {
      return {
        red: 0 as number,
        green: 0 as number,
        blue: 0 as number,
        opacity: 0 as number,
        generatedColor: '' as string,
        invertedColor: '' as string,
        displayInvertedColor: false as boolean,
        warmColor: false as boolean,
        coldColor: false as boolean
      }
    },
    components: {
      GenerateColors
    },
    created() {
      this.randomColor();
    },
    methods: {
      randomColor(): void {
        this.red = this.randomNumber();
        this.green = this.randomNumber();
        this.blue = this.randomNumber();
        // Experimental way to determine color temperature
        if (this.warmColor) {
          if (this.red < this.blue+50 && this.blue < 125) this.randomColor();
        } else if (this.coldColor) {
          if(this.red > this.blue+50 && this.red < 125) this.randomColor();
        }
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
  @import '../styles/main.less';

  .generate-colors-container {
    display: flex;
    justify-content: center;
    margin: 0.5em 0.5em 0 0.5em;
    flex-shrink: 0;
    flex-flow: row wrap;
    .generate-colors {
      margin: 0.5em 0.5em 0 0.5em;
    }
  }
  .color-options {
    width: @form-width;
    text-align: left;
    margin: 1em auto;
    display: flex;
    justify-content: center;
    flex-direction: column;
    div {
      margin: 0 auto;
    }
    
    .color-option {
      margin: @row-distance-margin;
      input {
        margin-left: 0;
      }
    }
    .generator-button {
      .button-styling;
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