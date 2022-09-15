<template>
  <div id="app">

    <input type="text" v-model="newTodoItem" @keydown = "addTodo">


    <!-- CRUD(크루드) / 웹의 기본적인 기능
    1. C: Create
    2. R : Read
    3. U : Update
    4. D : Delete -->
    
    
    <table>
      <thead>
        <tr>
          <th>No.</th>
          <th>TODO</th>
          <th>DONE</th>
          <th>EDIT</th>
          <th>DELETE </th>        
        </tr>
      </thead>

      <tbody>
        <tr v-for="(todo, index) in todoList" :key="'todo_' + todo.id">
          <td>{{todo.id}}</td>
          <td v-if="todo.isEdit === false">{{todo.todo}}</td>
          <td v-else>
             <input 
                type="text" 
                :placeholer="todo.todo" 
                v-model="editTodoItem"
                @keydown="editTodoText($event, index)"
                 /></td>
          <td @click="toggleStatus(index)">{{todo.isCompleted}}</td>
          <td><button @click="editTodo(index)">EDIT</button></td>
          <td><button @click="deleteTodo(index)">DELETE</button></td>
        </tr>
      </tbody>
    </table>




  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      newTodoItem : "",
      editTodoItem: "",

      todoList : [
      {
        id: 1,
        todo:'Study Javascript',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 2,
        todo:'Do Homework',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 3,
        todo:'Taeke a shower',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 4,
        todo:'Brush Teeth',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 5,
        todo:'Call my mom',
        isCompleted: false,
        isEdit: false,
      },
    ],
  };
  },

  methods: {
    toggleStatus(index) {
      console.log("toggleStatus", index);

      // this.todoList[index].isCompleted =!this.todoList[index].isCompleted
      // 실무에서는 이렇게 하면 안된다.
      if(this.todoList[index].isCompleted) {
        this.todoList[index].isCompleted = false;

      } else {
        this.todoList[index].isCompleted = true;
      }
      
    },

    deleteTodo(index) {
      console.log("deleteTodo", index);

      this.todoList.splice(index, 1) 
    },

// 키다운 누를때 , 키업 손 뗄때, 키프레스 엔터 인식
    // keyDown(e) {
    //   console.log('keyDown', e)
    // },

    // keyPress(e) {
    //   console.log('keyPress', e)
    // },

    // keyUp(e) {
    //   console.log('keyUp', e)
    // },
      addTodo(e) {

        let length = this.todoList.length;
        console.log('length',length);

        if(e.keyCode === 13){
          let newTodoObj = {
            // id: this.todoList.length + 1,
            id : this.todoList[this.todoList.length - 1].id + 1,
            todo : this.newTodoItem,
            isCompleted : false,
            isEdit: false,
          };

          this.todoList.push(newTodoObj);
          this.newTodoItem = "";
        }
      },
    
      editTodo(index) {
        console.log("index", index);
        this.todoList[index].isEdit =!this.todoList[index].isEdit;
      },

      editTodoText(e, index) {
        console.log("editTodoText");

        if(e.keyCode ===13) {
          this.todoList[index].todo = this.editTodoItem;
          this.todoList[index].isEdit = !this.todoList[index].isEdit;
          this.editTodoItem = "";
        }
      },
  
  },
};
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

table thead tr th {
  height: 30px;
  background-color:black;
  color:white;
}

table thead tr th:nth-child(2) {
  width: 150px;
}

table tbody tr{
  height: 30px;
}

table tbody tr:nth-child(odd) {
  background-color :#cccccc;
}

table tbody tr:hover {
  background-color:lightgreen;
  cursor : pointer;
}

input {
  margin-bottom:20px;
  padding: 10px;
  font-size:14px;
  border-radius: 10px;
  border: 1px solid lightgrey;
}
</style>
