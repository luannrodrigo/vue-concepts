<template>
  <div>
    <h1>My task list</h1>
    <button @click="handleShowTaskList">Show list</button>
    <br />
    <input 
        type="text" 
        @keyup.enter="addTask"
        v-focus 
        v-model="state.current"
    >
    <ul v-if="state.showList">
        <li 
            v-for="(task, index) in state.tasks"
            @dblclick="complete(task)"
            :key="`${task}-${index}`"
            class="cursor"
            :class="{
                'line-through' : task.isDone
            }"
        >
            {{ task.name }}
            <button @click="remove(task)">&times;</button>
        </li>
    </ul>
    <p v-else>Anonimous list task</p>
  </div>
</template>

<script>
import { reactive } from 'vue'
const focus = {
    inserted: (el) => {
        el.focus()
    }
}
export default {
    directives: {
        focus
    },
    setup () {
        const state = reactive({
            currentTask: '',
            showList: false,
            tasks: [{name: 'Curso', isDone: false}]
        })
        function handleShowTaskList() {
            state.showList = !state.showList
        }
        function addTask() {
            state.tasks.push({
                name: state.current,
                isDone: false
            })
            state.current = ''
        }
        function complete(task) {
            state.tasks = state.tasks.map(t => {
                if (t.name === task.name) {
                    return { ...t, isDone: !t.isDone }
                }
                return { ...t }
            })
        }
        function remove(task) {
            state.tasks = state.tasks.filter(t => t !== task)
        }

        return {
            state,
            handleShowTaskList,
            addTask,
            complete,
            remove
        }
    }
}
</script>

<style scoped>
    .line-through {
        text-decoration: line-through;
    }
    .cursor {
        cursor: pointer;
    }

</style>