<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import io from 'socket.io-client'
import Echo from 'laravel-echo';
import { onMounted, ref } from 'vue';
window.io = io

const test = ref([])
// console.log(io('http://chatrealtime.vn:6001'));
onMounted(() => {

  // let recaptchaScript = document.createElement('script')
  // recaptchaScript.setAttribute('src', 'http://chatrealtime.vn:6001/socket.io/socket.io.js')
  // document.head.appendChild(recaptchaScript)

  window.Echo = new Echo({
    broadcaster: 'socket.io',
    host: 'http://chatrealtime.vn:6001',
  })
  console.log(window.Echo);

  window.Echo.channel('laravel_database_chatroom').listen('MessagePosted', (data: any) => {
      test.value.push('test');
    })
})

</script>

<template>
  <div>
    <div v-for="(item, index) in test" :key="index">{{ item }}</div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
