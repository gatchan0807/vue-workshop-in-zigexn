<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h2>{{ randomNumber }}</h2>
    <h2 v-if="randomNumber >= 50">50以上やで</h2>
    <h2 v-if="randomNumber < 50">50より小さいで</h2>

    <form onsubmit="return false;" @submit="add">
      <input type="text" v-model="input">
      <button type="submit">追加</button>
    </form>

    <ul>
      <li v-for="todo in todos" v-bind:key="todo.contents">
        <input type="checkbox" name="status" id="status" v-model="todo.status" @click="toggle(todo.id)">
        <label :class="{done: todo.status}" for="status">{{todo.contents}}</label>
      </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios'
const BASE_URL = 'http://localhost:3000'
const url = BASE_URL + '/todos'

export default {
	name: 'HelloWorld',
	mounted: function() {
		axios.get(url).then(response => {
			this.todos = response.data
		})
	},
	computed: {
		randomNumber: function() {
			return Math.floor(Math.random() * 100) // 0〜100のランダムな値を返す
		},
	},
	data() {
		return {
			msg: 'このアプリは最高のアプリさ！',
			input: '',
			todos: [],
		}
	},
	methods: {
		add: function() {
			if (this.input.length === 0) {
				return
			}

			let newTodo = {
				contents: this.input,
				status: false,
			}

			axios
				.post(url, newTodo)
				.then(response => {
					alert('登録完了しました')
				})
				.catch(error => {
					alert('登録に失敗しました')
					console.error(error)
				})

			this.todos.push(newTodo)

			this.input = ''
		},
		toggle: function(_id) {
			let todo = this.todos.find(todo => {
				return todo.id === _id
			})

			todo.status = !todo.status

			axios.put(url + '/' + _id, todo)
		},
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
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

.done {
	text-decoration: line-through;
}

button {
	background-color: #42b983;
	color: #fff;
	border: 0;
}
</style>
