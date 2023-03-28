<template>
  <div class="main-block">
    <transition-group name="list" tag="div" class="list-items">
      <div v-for="index in count" :key="index" >
        <Counter msg="Welcome to Your Vue.js App"/>
      </div>
      <button class="add" v-on:click="addComponent" :key="1">
        <svg xmlns="http://www.w3.org/2000/svg" fill="#fff6" width="20px" height="20px" viewBox="0 0 1920 1920">
          <path d="M915.744 213v702.744H213v87.842h702.744v702.744h87.842v-702.744h702.744v-87.842h-702.744V213z" fill-rule="evenodd"/>
        </svg>
      </button>
    </transition-group>
  </div>
</template>

<script>
import Counter from './components/Counter.vue'

export default {
  name: 'App',
  components: {
    Counter
  },
  data() {
    return {
      count: 1
    };
  },
  methods: {
    addComponent() {
      this.count += 1;
    }
  }
}
</script>

<style>
body {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background-color: #353638;
}
#app {
  margin: 0 auto;
  color: #ffff;
  background-color: #353638;
  height: calc(100vh - 20px);
  width: 100%;
  text-align: center;
  max-width: 1024px;
  padding-top: 72px;
  font-weight: 400;
}
.add {
  width: 225px;
  height: 120px;
  background: #696969;
  border: none;
}
.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
}
.list-items {
  display: contents;
}
.main-block {
  display: grid;
  grid-template-columns: repeat(auto-fill,225px);
  grid-auto-flow: row dense;
  gap: 45px 50px;
  place-content: center;
}
</style>
