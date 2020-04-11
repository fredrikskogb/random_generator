<template>
  <div>
    <GenerateStrings :consonants="consonants"
                     :vowels="vowels"></GenerateStrings>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import GenerateStrings from '@/components/GenerateStrings.vue';

  export default Vue.extend({
    name: 'Strings',
    components: {
      GenerateStrings
    },
    data() {
      return {
        consonants: [] as string[],
        vowels: [] as string[]
      }
    },
    created() {
      this.setConsonants();
      this.setVowels();
    },
    methods: {
      setConsonants(): void {
        this.consonants = [
          "B", "C", "D", "F", "G", "H", "J", "K", "L", "M", "N", "P", "Q", "R", "S", "T", "V", "X", "Z", "W"
        ];
      },
      setVowels(): void {
        this.vowels = [
          "A", "E", "I", "O", "U", "Y"
        ];
      }
    }
  })
</script>

<style scoped>

</style>