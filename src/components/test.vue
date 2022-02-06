<template>
  <div id="app">
    <input placeholder="name" v-model="form.name" /><br />
    <input placeholder="yumFactor" v-model="form.yumFactor" /><br />
    <input placeholder="imageUrl" v-model="form.imageUrl" /><br />
    <input placeholder="comment" v-model="form.comment" /><br />
    <button @click="send">Send</button>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data: () => ({
    form:  {
      name: '',
      yumFactor: '',
      imageUrl: '',
      comment: ''
    }
  }),
  methods: {
    send(){      
      axios.post("https://samuel-davidson.co.uk/mmmDelicous/backend/4cZjLcFQgmAZ6gKr/newfileSSEP.php", this.form)
          .then(res => {
            console.log(res)
          }).catch(e => {
            console.log(e);
          })
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
