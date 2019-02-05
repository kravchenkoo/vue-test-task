<template>
    <div class="todo">
        <h1 class="title">Checklist</h1>
        <ul class="tasks">
            <li v-for="(task, index) in tasks" :class="{complete : task.complete}" @click="mounted">
                <label>
                    <ui-checkbox type="checkbox" v-model="task.complete"><!-- v-show="!task.complete" -->
                        {{task.name}}
                    </ui-checkbox>
                </label>
            </li>
        </ul>
        <div>
            <ui-textbox class="textbox" placeholder="e.g. 'read vue.js guide'" v-model="newTaskName"></ui-textbox>
            <ui-button class="button-add" color="primary" @click="addTask" icon="add">Add</ui-button>
        </div>
        <ui-progress-linear
                    color="black"
                    type="determinate"

                    :progress="progress"

                    v-show="isLoading"
                ></ui-progress-linear>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                newTaskName : '',
                tasks : [
                    {name : 'create skeleton of todo', complete : true},
                    {name : 'add ability to add tasks', complete : true},
                    {name : 'clear task name after clicking "Add"', complete : true},
                    {name : 'put "Add" button in one line with input', complete : true},
                    {name : 'add new task by hitting Enter instead of clicking "Add"', complete : false},
                    {name : 'replace <input> with <ui-checkbox> in tasks list', complete : true},
                    {name : 'when task is complete cross it out', complete : false},
                    {name : 'split tasks into "pending" and "complete" tabs using keen-ui component <ui-tabs>', complete : false},
                    {name : 'don\'t allow to add empty tasks', complete : false},
                    {name : 'make list of tasks scrollable, if there\'re are a lot of tasks', complete : false},
                    {name : 'extract list item into a separate vue.js component', complete : false},
                    {name : 'persist tasks list in a local storage', complete : false},
                    {name : 'add animation on task completion', complete : false},
                ],
                progress: 0,
                isLoading: true,
                progressInterval: null
            }
        },

        methods : {
            addTask () {
                this.tasks.push({name : this.newTaskName, complete : false});
                this.newTaskName = '';
            },
            remove(id) {
                this.tasks.splice(id,1);
            },
           mounted(numberIndex) {
                this.progressInterval = setInterval(() => {
                    if (this.progress = 1000) {
                        this.progress = 1000;
                    } else {
                        this.progress += 0.01;
                    }
                }, 10);

            }
        }
    };
</script>

<style scoped lang="scss">
    .todo {
        margin: auto;
        background: #fff;
        padding: 20px;
        border-radius: 5px;
        box-shadow: rgba(0, 0, 0, 0.3) 3px 3px 15px;

        .title {
            margin-top: 0;
        }

        .tasks {
            list-style: none;
            padding: 0;
        }
        .textbox {
            width: 80%;
            float: left;
        }
        .button-add {
            width: 20%; 
            loat: left;
            border-radius: 20px;
        }
    }
</style>
