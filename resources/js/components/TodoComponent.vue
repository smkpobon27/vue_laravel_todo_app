<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card">
                    <div class="card-header">Todo App</div>

                    <div class="card-body">
                        <form @submit.prevent="addTask">
                            <div class="input-group mb-3 input-group-sm">
                                <input type="text" v-model="inputAdd" class="form-control" placeholder="Add task to your list">
                                <div class="input-group-append">
                                    <button class="btn btn-primary btn-sm" type="submit">Add</button>
                                </div>
                            </div>
                        </form>

                        <div class="row">
                            <div class="col-md-6">
                                <h6>Your Tasks:</h6>
                            </div>
                            <div class="col-md-6">
                                <button type="button" v-show="!isSearch" @click="isSearch = true" class="btn btn-default btn-sm float-end "><i class="fa-solid fa-magnifying-glass"></i></button>
                                   
                                <div class="input-group mb-3 input-group-sm" v-show="isSearch">
                                    <input type="text" v-model="searchInput" class="form-control" placeholder="Search your task">
                                    <div class="input-group-append">
                                        <button class="btn btn-outline-secondary btn-sm" @click="isSearch = false; searchInput=null" type="button"><i class="fa-solid fa-xmark"></i></button>
                                    </div>
                                </div>
                            </div>
                        </div>  <!-- row end -->

                        <div class="row">
                            <div class="col-md-12">
                                    <div v-for="(task, index) in taskList" :key="index" class="input-group-prepend mb-1">
                                        <div class="input-group-text">
                                            <input type="checkbox" v-model="task.isComplete" :value="true"> &nbsp; <span :class="{'text-decoration-line-through' : task.isComplete}">{{task.value}}</span>
                                        </div>
                                    </div>

                                    <p class="text-center mt-3 mb-3" v-show="tasks.length == 0">You have no tasks <i class="fa-regular fa-face-grin-tears"></i> </p>
                            </div>
                        </div>  <!-- row end -->

                        <div class="row">
                            <div class="col-md-2">
                                <button type="button" @click="clearAll" class="btn btn-primary btn-sm mt-4">Clear All</button>
                            </div>
                        </div> <!-- row end -->
                    </div> <!-- card end -->
                </div>
            </div>
        </div>
    </div>
</template>


<script>
    export default {

        data(){
            return{
                tasks: [],
                inputAdd: null,
                isSearch: false,
                searchInput: null,
            }
        },

        mounted() {
            console.log('Component mounted.')
        },

        methods: {
            addTask(){
                this.tasks.push({
                    value: this.inputAdd,
                    isComplete: false,
                });
                this.inputAdd = null;
                console.log(this.tasks);
            },
            taskComplete(){

            },
            removeTask(index){
                this.tasks.splice(index, 1);
            },
            clearAll(){
                // this.tasks.splice(0);
                this.tasks = [];
            },
           
        },

        computed : {
             taskList(){
                if(this.searchInput){
                    return this.tasks.filter(task => {
                        return task.value.toLowerCase().includes(this.searchInput.toLowerCase())
                    })
    
                }else{
                    return this.tasks;
                }
            }
        }

    }
</script>



<style scoped>
.input-group-text {
    display: flex;
    align-items: center;
    padding: 0.375rem 0.75rem;
    font-size: 0.9rem;
    font-weight: 400;
    line-height: 1.6;
    color: #212529;
    text-align: center;
    white-space: nowrap;
    background-color: whitesmoke;
    border: 0px solid #ced4da;
    border-radius: 0.25rem;
}
</style>