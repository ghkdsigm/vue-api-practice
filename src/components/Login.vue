<template>
  <div>
    <input type="text">
    <button type="button" @click="loginUser">로그인</button>
    <button type="button" @click="loginUser1">로그인</button>
    <ul>
      <li v-for="item in items" :key="item" >
        {{item}}
      </li>
    </ul>   
  </div>
</template>

<script>
import axios from 'axios'
import { handlerException } from '../utils/handler.js'

export default {
  data(){
    return{
      items:[],
    }
  },
  methods:{
    //promise 비동기
    loginUser(){
      axios.get('https://jsonplaceholder.typicode.com/users/1')
      .then(res =>{
        if(res.data.id === 1){
          console.log('사용자가 인증됨')
          axios.get('https://jsonplaceholder.typicode.com/todos')
          .then(res =>{
            this.items = res.data
          })          
        }
      })
      .catch(err=>{
        console.log(err)
      })
    },
    //async await 비동기 방식
    async loginUser1(){
      try {
        const response = await axios.get('https://jsonplaceholder.typicode.com/users/1')
        if(response.data.id === 1){
          console.log('사용자가 인증됨')
          const list = await axios.get('https://jsonplaceholder.typicode.com/todos')
          this.items = list.data;
        }
      } catch (error) {
        handlerException(error)
      }      
    }
  }
}
</script>

<style>

</style>