<!-- Please remove this file from your project -->
<template>
  <div class="todo__block">

    <h1>This is the todo list</h1>

    <div class="create__block">
      <span @click="showCreate()" v-show="!isShowCreate">+ Create Todo</span>
      <div class="create__action" v-show="isShowCreate">
        <input type="text" v-model="newTodo" placeholder="Điền công việc bạn muốn làm">
        <button @click="addTodo()">Thêm</button>
      </div>
      
    </div>

    <span class="current__todo">
      Current active todos : {{ todoList.length > 0 ? todoList.length : 0}}
    </span>

    <div class="list__block">
      <div v-for="(todos,index) in todoList" :key="index" class="list__item" :class="{done: todos.done}">
        <span :class="{done: todos.done}" @click="todos.done = !todos.done">{{todos.todo}}</span>
        <div class="button__action">
          <button class="button__action--delete" @click="deleteTodo(index)">Xóa</button>
          <button class="button__action--edit" :disabled="todos.done" :class="{disabled: todos.done}">Sửa</button>
          <button class="button__action--done" :disabled="todos.done">Xong</button>
        </div>
        
      </div>
    </div>
    
  </div>
</template>

<script>
export default {
data(){
  return{
    isShowCreate: false,
    newTodo: "",
    todoList: [
      { todo: "Ăn sáng", done: false},
      { todo: "Uống thuốc", done: false},
      { todo: "Làm việc", done: false},
      { todo: "Ăn trưa", done: false},
      { todo: "Cho chó ăn", done: false},
    ]
  }
},
methods: {
  addTodo: function(){
    if(this.newTodo != ""){
      this.todoList.push({
        todo: this.newTodo, 
        done: false
      })
      this.newTodo = "";
      this.isShowCreate = !this.isShowCreate
    }
    
  },
  deleteTodo: function(index) {
      this.todoList.splice(index, 1)
  },
  showCreate: function(){
    this.isShowCreate = !this.isShowCreate
  }
}
}
</script>

<style scoped>
h1{
    font-weight: normal;
    text-align: center;
  }
.todo__block{
  margin: auto;
  max-width: 500px;
}

.create__block{
  margin-bottom: 10px;
}
.create__block .create__action{
  display:flex;
  border: 2px solid #60C191;
  border-radius: 25px;
  padding: 5px 20px;
}
.create__block .create__action button{
  border: none;
  color: #60c191;
}
.create__block span{
  font-size: 20px;
  color: #60C191;
  font-weight: 200;
  cursor: pointer;
}
.create__block input{
  font-size: 20px;
  width: 100%;
  border: none
}
.create__block input:focus{
  outline: none;
}
.create__block button{
  font-size: 16px;
  margin-left: 5px
}

.current__todo{
  font-size: 20px;
}
.list__block{
  margin-top: 10px;
}
.list__item span{
  font-size: 20px;
  font-weight: 200;
  color: #60C191;
  cursor: pointer;
}
.list__item span.done{
  text-decoration: line-through;
  color: gray!important;
}

.list__item{
  display: flex;
  justify-content:space-between;
  margin-bottom: 10px;
  border: 2px solid #60C191;
  border-radius: 25px;
  padding: 5px 20px;
}
.list__item.done{
  border: 1px solid gray!important;
}


.list__item:last-child{
  margin-bottom: 0px;
}

.button__action button.button__action--delete,
.button__action button.button__action--edit,
.button__action button.button__action--done{
  font-size:16px;
  cursor: pointer;
  border: none;
}
.button__action button.button__action--delete{
  color: red;
}
.button__action button.button__action--edit{
  color: blue;
}
.button__action button.button__action--edit.disabled{
  color: gray!important;
}
.button__action button.button__action--done{
  color: #60C191;
}
</style>
