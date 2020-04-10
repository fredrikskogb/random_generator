<template>
  <div class="home">
    <div id="sub-nav"
         class="nav">
      <router-link to="/colors"
                   class="sub-nav-link">Colors & Color Schemes</router-link> |
      <router-link to="/tones"
                   class="sub-nav-link">Musical Tones and Melodies</router-link>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  components: {

  }
}
</script>
<style lang="less" scoped>
  #sub-nav {
    padding: 0;
    .sub-nav-link {
    }
  }
</style>
