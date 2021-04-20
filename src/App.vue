<template>
  <div class=" custom-container  mx-auto d-flex flex-column ">
    
      <h1>To Do List </h1>

    <div v-if="!isEditing">
      <input type="text" v-model="todo" ref="taskInput" class="mx-2 my-2 custom-input" v-on:keyup.enter="storeTodo"><br>
    <input type="submit" class="btn-info"  value="اضافه کردن" @click="storeTodo">
    
    </div>
    <div v-else>
      <input type="text" v-model="todo" ref="taskInput" class="mx-2 my-2 custom-input" v-on:keyup.enter="updateTodo"><br>
    <input type="submit" class="btn-info" value="اعمال ویرایش" @click="updateTodo">
    
    </div>
    <br>
    <br>
    

    <ol>
      <li v-for="(todo,index) in todos" :key="todo.index" >
        {{todo}}
        <button @click="editTodo(index,todo)" class="btn btn-warning mx-2 my-2">ویرایش</button>
        <button @click="deleteTodo(index)" class="btn btn-danger">حذف</button>
      </li>
    </ol>
  </div>
</template>

<script>
export default {  
     data: () => ({
      isEditing:false,
      selectedIndex: null, 
      todo:'',
      todos:['مطالعه کتاب', 'برنامه نویسی'] 
       }),
        mounted() {
    this.focusInput();
  },
 
  methods:{
    storeTodo(){
      if(! this.todo) return;

      this.todos.push(this.todo);
      this.todo=''
    },

    editTodo(index,todo){
      this.todo=todo;
      this.selectedIndex= index;
      this.isEditing=true;
    },

    updateTodo(){
      this.todos.splice(this.selectedIndex , 1 , this.todo);
      this.isEditing=false;
      this.todo=""
    },

    deleteTodo(index){
      this.todos.splice(index , 1)
    },
    focusInput(){
            this.$refs.taskInput.focus();

    }

  }
}
</script>

<style>
        .custom-container {
          direction: rtl;           
                      max-width: 750px;
        }
        .custom-input{
          width:100%;
        }
        h1 {
        	padding-top: 40px;
        }
    </style>