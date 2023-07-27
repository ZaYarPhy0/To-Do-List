<template>
  <div class="bg-secondary mb-5" style="min-height: 100vh;">
    <h3 class="text-dark text-center bg-primary mb-5 py-3">To Do List Project</h3>
    <div class="mt-3 row">
      <div class="col-6 offset-3">
        <div class="row">
          <div class="col-6">
            <input type="text" class="form-control" v-model="name" v-on:keyup.enter="addTask">
          </div>
          <div class="col-4">
            <input type="button" value="Add" class="btn btn-success" v-on:click="addTask">
            <input type="button" value="delete" class="btn btn-danger ms-2" v-on:click="deleteTask">
          </div>
        </div>
        
        <div class="bg-light shadow-lg p-3 mt-5 rounded">
          <div class="" v-if="filterTask.length>0">
              <div class="row mt-4">
                <div class="col-6">
                  <h5>Task</h5>
                </div>
              <div class="col-6">
                <h5>Done</h5>
              </div>
            </div>
            <hr>
            <div class="row mt-4" v-for="(task,index) in filterTask" :key="index">
              <div class="col-6">
                <p :class="task.done?'delete':''">{{ task.action }}</p>
              </div>
              <div class="col-1">
                <input type="checkbox" v-model="task.done">
              </div>
            </div>
          </div>
          <div class="" v-else>
            <h5>There is no tasks.</h5>
          </div>
        </div>
        <div class="mt-4 row bg-danger p-2 rounded">
          <div class="col-6">
            <h5 class="">Hide Complete Task</h5>
          </div>
          <div class="col-1">
            <input type="checkbox" v-model="hiddenTask">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data:()=>({
    name:"",
    tasks:[],
    hiddenTask:false,
  }),
  computed: {
    filterTask(){
      return this.hiddenTask?this.tasks.filter((v)=>!v.done):this.tasks;
    },
  },
  methods:{
    addTask(){
      if(this.name!==""){
        this.tasks.push({action:this.name,done:false});
        this.storeData();
        this.name="";

      }else{
        alert("Enter Task");
      }
      
    },
    deleteTask(){
      this.tasks=this.tasks.filter((v)=>!v.done);
      this.storeData();

    },
    storeData(){
      localStorage.setItem("localDisk",JSON.stringify(this.tasks));
    }
  },
  mounted () {
  let data=localStorage.getItem("localDisk");
  if(data !== null){
    this.tasks=JSON.parse(data);
  }
},

}


</script>
<style>
.delete{
  text-decoration :line-through;
}
</style>
