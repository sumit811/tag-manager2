<template>
  <h1>Tag Manager </h1>
  <form @submit.prevent="addTag">
    <input type="text" v-model="tag">
    <input type="submit" value="Add Tag">
  </form>
  <h2>Tags List</h2>
  <ul v-if="tagslist.length>0">
    <li v-for="(tag,index) in tagslist" :key="index">
      {{tag}}<span @click="deletetag(index)">delete-{{index}}</span>
    </li>
  </ul>
  <p v-else>
    No tags found.
  </p>
</template>

<script>

export default {
  name: 'Tag-Manager',
  data(){
    return{
      tag:'',
      tagslist:[]
    }
  },
  mounted(){
    if(localStorage.getItem('tags')){
      console.log('localstorage',localStorage.getItem('tags'));
      this.tagslist = JSON.parse(localStorage.getItem('tags'))
    }
  },
  methods:{
    saveDataLocalStorage(tags){
      localStorage.setItem('tags', JSON.stringify(tags));
    },
    addTag: function(){
      this.tagslist.push(this.tag);
      this.tag='';
      this.saveDataLocalStorage(this.tagslist)
    },
    deletetag: function(did){
      this.tagslist.splice(did,1);
      this.saveDataLocalStorage(this.tagslist)
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
