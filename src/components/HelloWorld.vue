<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ randomNumber }}</h2>
    <h2 v-if="randomNumber >= 50">50以上やで</h2>
    <h2 v-if="randomNumber < 50">50より小さいで</h2>
  
    <ul>
      <li v-for="todo in todos" v-bind:key="todo.contents">
        <input type="checkbox" name="status" id="status" v-model="todo.status">
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
          status: false,
        },
        {
          contents: "Todo 2",
          status: false,
        },
        {
          contents: "Todo 3",
          status: false,
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
