
<template>
    <div class="root">
       <center> <h1>{{ title }}</h1> </center>

        <div class="input-group mb-3 task-form">
            <input type="text" class="form-control" placeholder="Введите задачу" v-model="formText">
            <button type="button" class="btn btn-primary" @click="add">Добавить</button>
        </div>

        <div class="alert alert-light" v-if="!taskList.length">
            У вас нету активных задач
        </div>
        <ul class="list-group" >
            <li class="list-group-item" v-for="(task, index) in taskList">
                    {{ task }}
                    <button type="button" class="close" @click="remove(index)">
                         <span aria-hidden="true">&times;</span>
                    </button>
            </li>
        </ul>
       <div class="count">{{ texts}} {{counter}}</div>
    </div>
</template>

<script>

    export default {
        data: function () {
            return {
                 taskList: [
                    'Task 1',
                    'Task 2 ',
                    'Task 3'
                ],
                formText: null, 
                title: 'Список задач',
                counter: null,
                texts: 'Количество активных задач равно ',
           }
        }, methods: {
            add: function () {
                if(!this.formText) {
                  return;
                }
                this.taskList.push(this.formText);
                  this.formText = null; 
                  this.save();
            } , 
            save: function () {
                localStorage.setItem('tasks', JSON.stringify(this.taskList));
            }  ,
            remove: function (index) { 
                this.taskList.splice(index, 1);
                this.save();
            }
        } , 
        created() {
            let storageData = localStorage.getItem('tasks');
            // console.log(storageData);
            this.taskList = JSON.parse(storageData);
            console.log(this.taskList.length);  
            this.counter=this.taskList.length;
        }
    }
</script>
<style>
body {padding:10%; background-color:#F5F5F5; }
 .task-list-container {
        max-width: 500px;
        margin: 0 auto;
    }
    .task-form {
        padding: 20px 0;
    }
  .count{
      padding-top:15px;
      font-size:30px;
      text-align:center;
  }
    
</style>