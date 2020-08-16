<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  //text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
html, .content{
    width: 80%;
    margin-right: auto;
    margin-left: auto;
    font-family: sans-serif;
    font-size: 16px;
    line-height: 1.5;
}
input,button,select,optgroup,textarea{
    font-family: inherit;
    font-size: inherit;
    line-height: inherit;
}
button {
    cursor: pointer;
    padding: 6px 12px;
    border-radius: 6px;
    color: #fff;
    border: 2px;
    background-color: #007bff;
    transition: background-color .2s;
}
button:hover{
    background-color: #0069d9;
}
button:active{
    background-color: #003c7c;
}
button:disabled{
    opacity: .5;
    pointer-events: none;
}
input{
    margin: 6px 2px;
    padding: 5px 12px;
    border-radius: 6px;
    color: #495057;
    border: 2px solid #ced4da;
}
textarea{
    margin: 6px 2px;
    padding: 5px 12px;
    width: 500px;
    height: 200px;
    border: 2px solid #ced4da;
}
select {
    border: 2px solid #ced4da;
}
/*추가*/
.my-header{
    background-color: steelblue;
    text-align: center; 
    font-size: 3em;
}
.my-header-blue{
    background-color: royalblue;
    text-align: center; 
    font-size: 3em;
    color: snow;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.small-button{
    padding: 0px 10px;
}
table{
    width: 100%;
    border-collapse: collapse !important;
}
tr>td:nth-child(1),tr>td:nth-child(3),tr>td:nth-child(4){
    width: 10%;
    text-align: center;
}
th{
    min-width: 50px;
}
#barchart_material{
    display: none;
}

</style>
