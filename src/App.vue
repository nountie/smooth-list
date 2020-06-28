<template>
  <div id="app">
      <div class="container">
        <h3 class="heading">Write sth down and click Enter. You can use hashtags to highlight. Click on an item to delete.</h3>
        <input placeholder="Type something" @keyup.enter="addTodo" v-model.lazy="newTodo">
        <transition-group tag="ul" name="compress">
          <AppToDo 
          @click.native="deleteToDo(index)"
          v-for="(todo, index) in todos" 
          :index="index" 
          :content="todo.content" 
          :key="`todo${todo.id}`"
          />
        </transition-group>
      </div>
  </div>
</template>

<script>
import AppToDo from './components/AppToDo.vue'

export default {
  name: 'app',
  components: {
    AppToDo
  },
  data() {
    return {
      newTodo: "",
      newId: 3,
      todos: [
        {id: 1, content: 'Example todo'},
      ],
      hashtags: [],
      hashtagIds: {}
    }
  },
  methods: {
    addTodo() {
      if(this.newTodo.length > 3) {
        const detectedHashtags = this.detectHashtags(this.newTodo);
        let todoContent = this.newTodo;
        if(detectedHashtags) {
          todoContent = todoContent.replace(/(#[\p{L}.0-9]*)/gu, '<b class="hashtag">$1</b>');
          this.addHashtags(detectedHashtags);
          detectedHashtags.forEach(index => {
            if(!this.hashtagIds[index]) this.$set(this.hashtagIds, index, []);
            this.hashtagIds[index].push(this.newId);
          });
        }
        this.newId++;
        this.todos.push({id: this.newId, content: todoContent});
        this.newTodo = "";
      }
    },
    detectHashtags(text) {
      return text.match(/#[\p{L}.0-9]*/gu);
    },
    addHashtags(hashtagsArray) {
      this.hashtags = this.hashtags.concat(hashtagsArray.filter((item) => this.hashtags.indexOf(item) < 0));
    },
    deleteToDo(index) {
      this.todos.splice(index, 1);
    } 
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
  background: #f9f9f9;
}
.hashtag {
  padding: 5px 7px;
  border-radius: 2px;
  color: #fff;
  background: #000;
  font-size: 14px;
  position: relative;
  top: -1px;
  margin-left: 4px;
}
ul li {
  display: inline-block;
  min-width: 100%;
}

input {
  outline: none;
  padding: 16px 20px;
  border: 1px solid #efefef;
  border-left: 0;
  border-right: 0;
  width: 100%;
  font-size: 19px;
  box-shadow:
    0 -0.9px 2.2px rgba(0, 0, 0, 0.011),
    0 -2.1px 5.4px rgba(0, 0, 0, 0.016),
    0 -3.9px 10.1px rgba(0, 0, 0, 0.02),
    0 -6.9px 18.1px rgba(0, 0, 0, 0.024),
    0 -13px 33.8px rgba(0, 0, 0, 0.029),
    0 -31px 81px rgba(0, 0, 0, 0.04);
}

.todo {
  transition: all .3s ease-in;
}

.heading {
  font-size: 13px;
  font-weight: 600;
}

ul {
  width: 100%;
  padding: 0;
  margin: 0;
  position: relative;
}

.container {
  width: 700px;
  margin: 0 auto;
  padding: 0;

}
</style>
