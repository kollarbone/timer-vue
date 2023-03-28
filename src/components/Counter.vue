<template>
    <div class="counter">
      <div class="count" v-bind:class="{ active: isRunning }">
        <p>{{ formattedElapsedTime }}</p>
      </div>
      <div class="buttons" v-bind:class="{ active: isRunning }">
        <button @click="start" v-if="isRunning">
          <svg xmlns="http://www.w3.org/2000/svg" fill="#ffffff" width="20px" height="20px" viewBox="-7 0 32 32" version="1.1">
            <title>play</title>
            <path d="M0 6.688v18.906c0 0.344 0.156 0.625 0.469 0.813 0.125 0.094 0.344 0.125 0.5 0.125s0.281-0.031 0.438-0.125l16.375-9.438c0.313-0.219 0.5-0.5 0.5-0.844 0-0.313-0.188-0.594-0.5-0.813l-16.375-9.438c-0.563-0.406-1.406 0.094-1.406 0.813z"/>
          </svg>
        </button>
        <button @click="stop" v-else>
          <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" fill="none">
            <path d="M9 19.75C8.80189 19.7474 8.61263 19.6676 8.47253 19.5275C8.33244 19.3874 8.25259 19.1981 8.25 19V5C8.25 4.80109 8.32902 4.61032 8.46967 4.46967C8.61032 4.32902 8.80109 4.25 9 4.25C9.19891 4.25 9.38968 4.32902 9.53033 4.46967C9.67098 4.61032 9.75 4.80109 9.75 5V19C9.74741 19.1981 9.66756 19.3874 9.52747 19.5275C9.38737 19.6676 9.19811 19.7474 9 19.75Z" fill="#ffffff"/>
            <path d="M15 19.75C14.8019 19.7474 14.6126 19.6676 14.4725 19.5275C14.3324 19.3874 14.2526 19.1981 14.25 19V5C14.25 4.80109 14.329 4.61032 14.4697 4.46967C14.6103 4.32902 14.8011 4.25 15 4.25C15.1989 4.25 15.3897 4.32902 15.5303 4.46967C15.671 4.61032 15.75 4.80109 15.75 5V19C15.7474 19.1981 15.6676 19.3874 15.5275 19.5275C15.3874 19.6676 15.1981 19.7474 15 19.75Z" fill="#ffffff"/>
          </svg>
        </button>
        <button @click="reset">
          <svg xmlns="http://www.w3.org/2000/svg" width="20px" height="20px" viewBox="0 0 24 24" fill="none"><path d="M20.2 3H3.8a.8.8 0 0 0-.8.8v16.4a.8.8 0 0 0 .8.8h16.4a.8.8 0 0 0 .8-.8V3.8a.8.8 0 0 0-.8-.8Z" fill="#ffffff"/></svg>
        </button>
      </div>
    </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      elapsedTime: 0,
      timer: undefined,
      isRunning: true
    };
  },
  computed: {
    formattedElapsedTime() {
      const date = new Date('December 17, 1995 00:00:00');
      date.setSeconds(this.elapsedTime / 1000);
      const utc = date.toUTCString();
      if (date.getMinutes(utc) === 0) {
        return date.getSeconds(utc.substr(utc.indexOf(":") - 2, 8));
      } else if (date.getMinutes(utc) !== 0 && date.getHours(utc) === 0) {
        return utc.substr(utc.indexOf(":") - -1, 6);
      }
      else {
        return utc.substr(utc.indexOf(":") - 2, 8);
      }
    },
  },
  methods: {
    start() {
      if (!this.timer) { 
        this.timer = setInterval(() => {
          this.elapsedTime += 1000;
          this.isRunning = false;
        }, 1000); 
      }
    },
    stop() {
      clearInterval(this.timer);
      this.isRunning = true;
    },
    reset() {
      this.elapsedTime = 0;
      this.isRunning = true;
    }
  },
};
</script>
<style>
.counter {
  width: 225px;
  height: 120px;
  background: #696969;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
p {
  font-weight: 400;
  font-size: 22px;
  line-height: 21px;
}
.count {
  height: 60px;
  width: 100%;
  border-bottom: 1px solid;
  transition: ease-in-out 0.5s;
}
.buttons {
  height: 60px;
  width: 100%;
  margin: 20px;
  transition: ease-in-out 0.5s;
}
.active {
  opacity: .4;
  transition: ease-in-out 0.5s;
}
.buttons button {
  background: none;
	color: inherit;
  border: none;
  margin-left: 20px;
  margin-right: 20px;
  cursor: pointer;
  transition: ease-in-out 0.5s;
}
</style>