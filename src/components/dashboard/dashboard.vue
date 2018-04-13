<template>
  <div id="dashboard">
    <h1>That's the dashboard!</h1>
    <p>You should only get here if you're authenticated!</p>
    <ul>
      <li
        v-for="user in users"
        :key="user.id"> Your Age: {{ user.age }} | Your Email: {{ user.email }}</li>
    </ul>
  </div>
</template>

<script>
  import axios from 'axios'

  export default{
    data(){
      return{
        email: '',
        users: [],
      }
    },
    beforeCreate(){
      console.log('load data from firebase..')
    },
    created(){
      axios.get('https://vue-learning-indrakusuma.firebaseio.com/users.json')
        .then(res => {
          console.log('berhasil ambil data..');
          let resultUsers = [];
          const data = res.data;
          for (let key in data){
            resultUsers.push(data[key]);
          }
          console.log('kirim data ke users..');
          this.users = resultUsers;
        })
        .catch(error => console.log(error))
    }
  }
</script>

<style scoped>
  h1, p {
    text-align: center;
  }

  p {
    color: red;
  }
</style>
