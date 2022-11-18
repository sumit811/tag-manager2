<template>
  <h1>Tag Manager </h1>
  <form @submit.prevent="addTag">
    <input type="text" v-model="tag">
    <p class="error" ref="error">Empty tag cannot be created</p>
    <input type="submit" value="Add Tag">
  </form>
  <h2>Tags List</h2>
  <ul v-if="tagslist.length > 0">
    <li v-for="(tag,index) in tagslist" :key="index">
      {{ tag }}<span @click="deletetag(index)">&#10007;</span>
    </li>
  </ul>
  <p v-else>
    No tags found.
  </p>
</template>

<script>

export default {
  name: 'Tag-Manager',
  data() {
    return {
      tag: '',
      tagslist: []
    }
  },
  mounted() {
    if (localStorage.getItem('tags')) {
      this.tagslist = JSON.parse(localStorage.getItem('tags'))
    }
  },
  methods: {
    saveDataLocalStorage(tags) {
      localStorage.setItem('tags', JSON.stringify(tags));
    },
    addTag: function () {
      if(this.tag.length>0){
        this.tagslist.push(this.tag);
        this.tag = '';
        this.saveDataLocalStorage(this.tagslist)
        this.$refs.error.style.display = "none";
      } else {
        this.$refs.error.style.display = "block";
      }
    },
    deletetag: function (did) {
      this.tagslist.splice(did, 1);
      this.saveDataLocalStorage(this.tagslist)
    }
  }
}
</script>

<style>
body{
  background: #6A1B9A;
  color: #FFFF00;
  height: 100vh;
  margin:0;
  text-align: center;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Rubik Microbe', cursive;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
h1{
  font-size: 36px;
}
h2{
  font-size: 28px;
}

input[type="text"] {
  width: calc(100% - 40px);
  max-width: 320px;
  display: block;
  margin: 10px auto;
  border: 0;
  border-radius: 4px;
  box-shadow: 0px 1px 7px 7px rgb(10 10 10 / 30%);
  padding: 20px 10px;
  font-size: 20px;
}
input[type="submit"] {
    margin: 20px auto;
    width: 200px;
    padding: 12px;
    font-size: 20px;
    font-weight: bold;
    font-family: inherit;
    /* background: linear-gradient(45deg, black, transparent); */
    border-radius: 10px;
    background: #FFFF00;
}
ul{
  list-style: none;
  width: calc(100% - 40px);
  max-height: 200px;
  height: auto;
  text-align: left;
}
li{
  font-family: Arial;
  display: inline-block;
  padding: 10px;
  margin-right: 20px;
  margin-bottom: 20px;
  border-radius: 3px;
  box-shadow: 0px 0px 4px 3px #ffff00;
}
li span{
  cursor: pointer;
  margin-left: 5px;
}
.error{
  display: none;
  margin: 0;
}
</style>
