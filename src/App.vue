<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input v-model="newItem" v-on:keyup.enter="addNew">
    <ul>
      <li v-for="item in items" :class="{ finished: item.isFinished }" v-on:click="toggleFinish(item)">
        {{ item.label + item.isFinished}}
      </li>
    </ul>
  </div>
</template>

<script>
    export default {
      data : function(){
        return {
          title: "hello VUE !",
          items: [
            // {
            //   label: 'coding',
            //   isFinished: false
            // },
            // {
            //   label: 'watchTV',
            //   isFinished: true
            // }
          ],
          newItem: ''
        }
      },

      methods : {
        toggleFinish: function (item){
          item.isFinished = !item.isFinished
        },
        addNew: function (){
          this.items.push({
            label: this.newItem,
            isFinished: false
          });
          console.log(this.newItem);
          this.newItem = '';
        }
      }

    }
</script>

<style>
.finished{
  text-decoration: underline;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
