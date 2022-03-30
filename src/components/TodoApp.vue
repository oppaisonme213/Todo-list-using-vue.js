<template>

  <div class="container" style="max-width: 600px">
    
    <div class="headerrs">
      <h2 class="text-center mt-5">TASK MANAGER</h2>
    </div>

    <!-- Input task -->
    <div class="d-flex mt-5">
      <input
        type="text"
        v-model="task"
        placeholder="Enter task"
        class="w-100 form-control"
      />
      <button class="btn btn-danger rounded-0 " @click="submitTask">
        {{ isUpdate ? 'Update' : 'Add' }}
      </button>
    </div>

    <!-- Task table (bootstrap table)-->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col" style="width: 120px">Status</th>
          <th scope="col" class="text-center">Delete</th>
          <th scope="col" class="text-center">Edit</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td class="width: 120px">
            <span @click="changeStatus(index)" class="pointer">
              {{ task.status }}
            </span>

          </td>
          
          <td class="text-center">
              <button @click="deleteTask(index)">
                <span class="fa fa-trash pointer"></span>
              </button>
          </td>
          <td class="text-center">   
              <button @click="editTask(index)">
                <p class="fa fa-pen pointer"></p>
              </button> 
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },

  data() {
    return {
      task: "",
      editedTask: null,
      taskStatuses:['to-do', 'in-progress', "finished"],
      isUpdate: false,
      tasks: [
        {
          name: "create to do application using vue",
          status: "to-do",
        },
        {
          name: "1 hour break",
          status: "in-progress",
        }
      ]
    }
  },
  methods: {
    submitTask() {
      if (this.task.length === 0) return;

      if(this.editedTask === null){
        this.tasks.unshift({
          name: this.task,
          status: "to-do",
        });  
      }
      else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }  
        this.isUpdate = false;        
        this.task = ''
    },
    deleteTask(index){
      this.tasks.splice(index, 1)
    },
    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
      this.isUpdate = true;
    },
    changeStatus(index){
      let newIndex = this.taskStatuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.taskStatuses[newIndex];
    }


  },
  watch:{
    task(newVal, oldVal){
      console.log("New Value", newVal)
      console.log("old Value", oldVal)
    }
  }
  
};
</script>

<style>
.pointer{
  cursor: pointer;
}

*{
  background-color: black;
  color: white;
}
.btnad{
  background-color: red;
}

</style>