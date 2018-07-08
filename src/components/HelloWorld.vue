<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ randomNumber }}</h2>
    <h2 v-if="randomNumber >= 50">50以上やで</h2>
    <h2 v-if="randomNumber < 50">50より小さいで</h2>
  
    <ul>
      <li v-for="todo in todos" v-bind:key="todo.contents">
        {{todo.contents}}
      </li>
    </ul>
  
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  computed: {
    randomNumber: function() {
      return Math.floor( Math.random() * 100 ) // 0〜100のランダムな値を返す
    }
  },
  data () {
    return {
      msg: 'このアプリは最高のアプリさ！',
      todos: [
        {
          contents: "Todo 1",
        },
        {
          contents: "Todo 2",
        },
        {
          contents: "Todo 3",
        },
      ],
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
