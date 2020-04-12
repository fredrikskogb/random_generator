<template>
  <div>
    <GenerateTones></GenerateTones>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue';
  import GenerateTones from '@/components/GenerateTones.vue';
  export default Vue.extend ({
    name: 'Tones',
    components: {
      GenerateTones
    }
  })
</script>

<style lang="less" scoped>

</style>