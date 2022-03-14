<template>
  <div id="app-main" :class="darkTheme ? 'bg-dark' : ''">
    <div class="form-check form-switch darkmode-switch">
      <input
        class="form-check-input"
        type="checkbox"
        role="switch"
        id="darkMode"
        @change="darkTheme = !darkTheme"
      />
      <label class="form-check-label" for="darkMode">{{
        darkTheme ? "Dark Mode" : "Light Mode"
      }}</label>
    </div>
    <h1>My Personal Notes</h1>
    <MyNotes />
  </div>
</template>

<script>
import MyNotes from "./components/Notes.vue";
export default {
  name: "App",
  components: {
    MyNotes,
  },
  data: () => {
    return {
      darkTheme: false,
    };
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Abel&display=swap");
*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  /* background: #0f2027;
  background: -webkit-linear-gradient(to right, #2c5364, #203a43, #0f2027);
  background: linear-gradient(to right, #2c5364, #203a43, #0f2027); */

  /* background: #2193b0;
  background: -webkit-linear-gradient(to right, #6dd5ed, #2193b0);
  background: linear-gradient(to right, #6dd5ed, #2193b0); */

  /* background: #a8c0ff;
  background: -webkit-linear-gradient(to right, #3f2b96, #a8c0ff);
  background: linear-gradient(to right, #3f2b96, #a8c0ff); */

  /* background: #000000;
  background: -webkit-linear-gradient(to right, #0f9b0f, #000000);
  background: linear-gradient(to right, #0f9b0f, #000000); */

  background: #780206;
  background: -webkit-linear-gradient(to right, #061161, #780206);
  background: linear-gradient(to right, #061161, #780206);
}
#app {
  /* font-family: Avenir, Helvetica, Arial, sans-serif; */
  font-family: "Abel", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
}
#app-main {
  padding-top: 60px;
  min-height: 100vh;
}
.bg-dark {
  background: #222;
  color: #fff;
}
.darkmode-switch {
  display: flex;
  justify-content: space-around;
  width: 120px;
  position: absolute;
  top: 5px;
  right: 5px;
}
</style>
