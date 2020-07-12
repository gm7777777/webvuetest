<template>
  <div id="app">
    <!--<div id="nav">-->
      <!--<router-link to="/">Home</router-link> |-->
      <!--<router-link to="/about">About</router-link>-->
    <!--</div>-->
    <!--<router-view/>-->
    <!--<p>ID:<input v-model="idstr" placeholder="idstr"></p>-->
    <p>URL:<input v-model="urlStr" placeholder="input your long url"></p>
    <p>COMMENT:<input v-model="comment" placeholder="input url comment"></p>
    <p> <button v-on:click="getShortenURL()">submit</button></p>
    <!--<p>TINY URL:<textarea v-model="shortenURL" placeholder="show tiny url"></textarea></p>-->
    <!--<p>TINY URL:<input type="text" v-model="shortenURL" /></p>-->
    <!--<p>{{ shortenURL }}</p>-->
    TINY URL:<textarea id="shortenURL" rows="5"cols="50" v-model="shortenURL" placeholder="show tiny url"></textarea>
    <p>UNIQUE RESOURCE ID:<input id='idstr' v-model="idstr" placeholder="idstr"></p>
    <p> <button v-on:click="getURLRecord()">checkRecord</button></p>
    RECORD URL:<textarea id="recordURL" rows=10 cols="50" v-model="recordURL" placeholder="show record url"></textarea>
  </div>
</template>

<script>
    import axios from 'axios';
  // import Vue from 'vue'
    // window.onload = function() {
    //     new Vue({
    //         el: '#app',
    //         data: {
    //             idstr: '',
    //             urlStr: '',
    //             comment: '',
    //             shortenURL: '',
    //         },
    //         // 在 `methods` 对象中定义方法
    //         methods: {
    //             getShortenURL: function () {
    //                 var instance = axios.create({
    //                     baseURL: 'http://localhost:9100',
    //                     timeout: 10000,
    //                     headers: {'Content-Type': 'application/json'},
    //                 });
    //                 instance.post("/getShortenURL", {
    //                     urlStr: this.urlStr,
    //                     comment: this.comment,
    //                 }).then(function (response) {
    //                     console.log(response.data.shortenURL);
    //                     this.shortenURL = response.data.shortenURL;
    //                     console.log(response);
    //                 })
    //                     .catch(function (error) {
    //                         console.log(error);
    //                     });
    //                 // alert(this.urlStr+this.comment+this.shortenURL);
    //                 // console.log(this.urlStr+this.comment+this.shortenURL);
    //             },
    //         }
    //     });
    // }

    export default {
        props:{
           idstr:{
               type: String,
               default: ''
           },
            urlStr:{
                type: String,
                default: ''
            },
            comment:{
                type: String,
                default: ''
            },
            shortenURL:{
                type: String,
                default: ''
            },
            recordURL:{
                type: String,
                default: ''
            }
        },
        methods:{
            getShortenURL: function(){
                var instance = axios.create({
                    // baseURL: 'http://192.168.232.137:9200',
                    baseURL: 'http://3.20.226.34:9200',
                    // baseURL: 'http://localhost:9100',
                    timeout: 10000,
                    headers: {'Content-Type': 'application/json'},
                });
                instance.post("/test",{
                // instance.post("/getShortenURL",{
                    urlStr:this.urlStr,
                    comment:this.comment,
                    }).then(function (response) {
                    // alert("Your tiny url is : "+response.data.shortenURL);
                    document.getElementById("shortenURL").value=response.data.shortenURL;
                    document.getElementById("idstr").value=response.data.id;
                    console.log(response);
                    })
                    .catch(function (error) {
                        console.log(error);
                    });
              // alert(this.urlStr+this.comment+this.shortenURL);
              // console.log(this.urlStr+this.comment+this.shortenURL);
            },
            getURLRecord: function(){
                var instance = axios.create({
                    // baseURL: 'http://192.168.232.137:9200',
                    baseURL: 'http://3.20.226.34:9200',
                    // baseURL: 'http://localhost:9100',
                    timeout: 10000,
                    headers: {'Content-Type': 'application/json'},
                });

                instance.post("/test1",{
                // instance.post("/getRecord",{
                    idStr:document.getElementById('idstr').value,
                }).then(function (response) {
                    // alert("Your tiny url is : "+response.data.shortenURL);
                    document.getElementById("recordURL").value=JSON.stringify(response.data);
                    console.log(response);
                })
                    .catch(function (error) {
                        console.log(error);
                    });
            }
        }
    }
</script>
<style lang="stylus">
#app
  font-family Avenir, Helvetica, Arial, sans-serif
   -webkit-font-smoothing antialiased
   -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
</style>
