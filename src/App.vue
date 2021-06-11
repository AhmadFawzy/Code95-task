<template>
  <div id="app">
    <AppHeader />
    <div class="container">
      <router-view/>
    </div>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
export default {
  components: {
    AppHeader
  },
  data() {
    return {
      appConfig: {
        "arabic": {lang: "AR", dir: "rtl"}
      }
    }
  },
  created() {
    let html = document.querySelector("html");
    html.setAttribute("lang", this.appConfig.arabic.lang);
    html.setAttribute("dir", this.appConfig.arabic.dir);
  }
}
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Harmattan:wght@400;700&display=swap');
  body {
    font-family: 'Harmattan', sans-serif;
  }
  // Font Variables :-
  $grayText01: #7F7F7F;
  // ======================
  // helper classes :-
  .pointer {
    cursor: pointer;
  }
  .required {
    color: red;
  }
  // ======================
</style>