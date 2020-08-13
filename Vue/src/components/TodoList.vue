<template>
  <div >
      <!--phut thu 33-->
      <input
       type="text"
        class="todo-input" 
        placeholder="What..."
        v-model="newTodo"
         @keyup.enter ="addTodo">
        <div v-for="(todo, index) in todos" :key="todo.id" 
        class="todo-item">
            <div class="todo-item-left">
            <div 
            v-if="!todo.editing" 
            class="todo-item-label"
            @dblclick="editTodo(todo)"> 
            {{ todo.title }}
            </div>
            <input v-else
              type="text" 
              class="todo-item-edit"
               v-model="todo.title"
               @blur="doneEdit(todo)"
               @keyup.enter="doneEdit(todo)"
               @keyup.esc="cancelEdit(todo)"
               v-focus>
            </div>
           <div class="remove-item"
            @click="removeTodo(index)">
           &times;
        </div>
        </div>
        

        Todo lis here
  </div>
</template>

<script>
export default {
  name: 'todo-list',
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      beforeEditCache: '',
      todos: [
          {
              'id': 1,
              'title': ' finish',
              'completed': false,
              'editing': false,
          },
          {
              'id': 1,
              'title': ' fin',
              'completed': false,
              'editing': false,
          }

      ]
    }
  },
  directives: {
      focus:{
          inserted: function(el){
              el.focus()
          }
      }
  },
  methods: {
      addTodo(){
          if(this.newTodo.trim().length == 0){

          }
          this.todos.push({
              id:this.idForTodo,
              title: this.newTodo,
              completed: false,
          })
          this.newTodo= '',
          this.idForTodo++
      },
      editTodo(todo){
          this.beforeEditCache = todo.title
          todo.editing=true
      },
      cancelEddit(todo){
          todo.title= this.beforeEditCache
          todo.editing= false
      },
      doneEdit(todo){
            if(todo.title.trim().length == 0){

          }
          todo.editing= false
      },
      removeTodo(index){
          this.todos.splice(index,1)
      }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
.todo-input{
    width: 100%;
    padding: 10pxx 18px;
    font-size: 18px;
    margin-bottom: 16px;
   
}  
.todo-input:focus{
    outline: 0;
} 

.todo-item{
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
.remove-item{
    cursor: pointer;
    margin-left: 14px;
}
.remove-item:hover{
    color:goldenrod;
}
.todo-item-edit{
    font-size: 12px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    font-family: 'Avenir', Arial, Helvetica, sans-serif;

}
.todo-item-edit:focus{
    outline: none;
}

</style>
