<template>
<div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <div v-if="showAddTask">
    <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="toogleReminder" @delete-task="deleteTask" :tasks="tasks"/>
</div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTask from './components/AddTask.vue';

export default {
  name: 'App',
  components:{
    Header,
    Tasks,
    AddTask
  },

   data(){
    return{
      tasks: [],
      showAddTask: false
    }
   } ,

    methods:{

      toggleAddTask(){
        this.showAddTask = !this.showAddTask;
      },

      addTask(task){
        this.tasks = [...this.tasks,task]
      },

      deleteTask(id){

        if(confirm('Are you sure?')){
             this.tasks = this.tasks.filter((task) => task.id !== id)
        }
    
      },

      toogleReminder(id){
       this.tasks = this.tasks.map((task) => task.id === id ?{...task, reminder: !task.reminder} : task)
      }
    },

   created(){
    this.tasks = [{
      id: 1,
      text: 'Doctors Appoitment',
      day: 'March 1st at 2:30',
      reminder:true
    },

    {
      id: 2,
      text: 'Meeting at school',
      day: 'April 1st at 2:30',
      reminder:true
    },

    {
      id: 3,
      text: 'Death',
      day: 'May 1st at 2:30',
      reminder:false
    }]

   }
}
</script>

<style>


*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: 'Poppins', sans-serif;
}

.container{
  max-width: 500px;
  margin:30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn{
  display: inline-block;
  background: #000;
  color:#fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

</style>
