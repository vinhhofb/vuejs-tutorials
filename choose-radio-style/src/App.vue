<template>
  <div :class="`body-box ${themes[count]}`">
    <div :class="`card ${themes[count]}-div`">
      <h1 class="title">{{ themes[count] }}</h1>
      <p class="description">Welcome to {{ themes[count] }}</p>
      <div class="box-chosse">
        <button v-for="(theme, index) in themes" :key="index" :data-theme="theme"
          :class="['button-class', { 'button-class-active': count === index }]" @click="changeTheme(theme)">
          <div class="title-selected">
            <label>{{ capitalized(theme) }}</label>
          </div>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      themes: ["Reactjs", "Vuejs", "Angular", "Nextjs"],
      count: 0,
    };
  },
  methods: {
    changeTheme(theme) {
      if (theme) {
        this.count = this.themes.indexOf(theme);
      } else if (this.count < 3) {
        this.count += 1;
      } else {
        this.count = 0;
      }
    },
    capitalized(word) {
      return word.charAt(0).toUpperCase() + word.slice(1);
    },
  },
  mounted() {
    this.changeTheme(this.themes[0]);
  },
};
</script>

<style>
.body-box{
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  padding: 2rem;
}
.Vuejs{
  background: #00bc7f;
}
.Vuejs-div{
  background: #3ed5a5;
}
.Reactjs{
  background: #027bfb;
}
.Reactjs-div{
  background: #56a4f7;
}
.Angular{
  background: #dd0031;
}
.Angular-div{
  background: #c3002f;
}
.Nextjs{
  background: #101214;
}
.Nextjs-div{
  background: #161a1d;
}
html {
  box-sizing: inherit;
  font-size: 62.5%;
}

.card {
  width: 100%;
  border-radius: 1.6rem;
  padding: 3.2rem;
}

.title {
  margin: 0 0 2rem;
  padding: 0;
  line-height: 1.2;
  font-size: 3.5rem;
  color: #dee4ea;
}

.description {
  margin: 0;
  padding: 0;
  line-height: 150%;
  font-size: 2rem;
  color: #738496;
}

.button-class {
  display: flex;
  width: 100%;
  flex-direction: column;
  background: #ececec;
  color: #738496;
  position: relative;
  padding: 1.6rem;
  border-radius: 1.2rem;
  user-select: none;
  cursor: pointer;
  transition: all 120ms ease-out;
  border:0;
}

.button-class:hover,
.button-class:focus {
  transform: scale(1.03);
}

.button-class-active {
  outline: 4px solid #1d7afc;
}

.button-class-active:after {
  content: "✓";
  position: absolute;
  top: -1.2rem;
  right: -1.2rem;
  height: 2.4rem;
  width: 2.4rem;
  background: #1d7afc;
  border-radius: 999px;
  color: #fff;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

.box-chosse {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 1.6rem;
  margin: 3.2rem 0;
}
</style>