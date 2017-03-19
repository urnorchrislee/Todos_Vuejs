<template>
  <div id="app">
    <h1>{{ title }}</h1>
    <input v-model="newItem" v-on:keyup.enter="addNew" placeholder="请输入内容">
    <ul>
      <li v-for="item in items" :class="{ finished: item.isFinished }" v-on:click="toggleFinish(item)">
        {{ item.label}}
      </li>
    </ul>
  </div>
</template>

<script>
    import Stroe from './store'
    console.log(Stroe);

    export default {
      data : function(){
        return {
          title: "HELLO VUE !",
          items: Stroe.fetch(),
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
          this.newItem = '';
        }
      },

      watch: {
          // 深度 watcher
          items: {
            handler: function (items) { 
              console.log(items);
              Stroe.save(items);
            },
            deep: true
          }
      }

    }
</script>

<style>

*{
  margin: 0;
  padding: 0;
  border: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  width: 600px;
  height: 1000px;
  border: 1px solid #e0e0e0;
  margin: 100px auto;
  padding: 20px;
}

#app input{
  width: 98%;
  height: 40px;
  font-size: 20px;
  border: 1px solid #e0e0e0;
  margin: 20px 0px;
}

#app ul li{
  height: 40px;
  line-height: 40px;
  list-style: none;
  font-size: 20px;
  border-bottom: 1px solid #e0e0e0;
  text-align: left;
}

.finished{
  text-decoration: underline;
}
</style>
