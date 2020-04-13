<template>
  <div class="strings-container">
    <div class="strings-form-container">
      <div class="strings-input-container">
        <input type="number"
               max="10"
               min="2"
               v-model="stringLength">
        <label> Enter length</label>
      </div>
      <button class="generator-button" @click="generateString">Generate</button>
      <p class="string-result"
         v-if="stringResult.length >= 2">{{stringResult}}</p>
    </div>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';

  export default Vue.extend ({
    name: 'GenerateStrings',
    props: ['consonants', 'vowels'],
    data() {
      return {
        stringLength: 2 as number,
        stringResult: '' as string
      }
    },
    methods: {
        generateString(): void {
          this.stringResult = '';

          for(let i = 0; i < this.stringLength; i++) {
            const consonant = this.consonants[Math.floor(Math.random() * this.consonants.length)];
            const vowel = this.vowels[Math.floor(Math.random() * this.vowels.length)];

            if(Math.random() < 0.5) {
              this.stringResult += consonant;
            } else {
              this.stringResult += vowel;
            }
          }
        }
    }
  })
</script>

<style lang="less" scoped>
  @import '../styles/main.less';
  .strings-container {
    display: flex;
    justify-content: center;
    .strings-form-container {
      label, input, button {
        margin: @row-distance-margin;
      }
      display: flex;
      flex-direction: column;
      align-items: center;
      width: @form-width;
      .strings-input-container {

      }
      .generator-button {
        .button-styling;
      }
      .string-result {
        margin-top: 1em;
        font-size: 150%;
      }
    }
  }

</style>