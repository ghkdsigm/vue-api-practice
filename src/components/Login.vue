<template>
  <div>
    <input type="text">
    <button type="button" @click="loginUser">로그인</button>
    <ul>
      <li v-for="item in users" :key="item" >
        {{item.name}}
      </li>
    </ul>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      users:[],
    }
  },
  methods:{
    loginUser(){
      axios.get('https://jsonplaceholder.typicode.com/users/1')
      .then(res =>{
        if(res.data.id === 1){
          console.log('사용자가 인증됨')
          this.users = res.data
        }
      })
      .catch(err=>{
        console.log(err)
      })
    }
  }
}
</script>

<style>

</style>