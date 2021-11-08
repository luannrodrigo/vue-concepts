<template>
  <div>
    <h1>My task list</h1>
    <button @click="handleShowTaskList">Show list</button>
    <br />
    <input 
        type="text" 
        @keyup.enter="addTask"
        v-focus 
        v-model="current"
    >
    <ul v-if="showList">
        <li 
            v-for="(task, index) in tasks"
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
const focus = {
    inserted: (el) => {
        el.focus()
    }
}
export default {
    directives: {
        focus
    },
    data: () => ({
        showList: false,
        tasks: [{name: 'Curso', isDone: false}],
    }),
    methods: {
        handleShowTaskList() {
            this.showList = !this.showList
        },
        addTask() {
            this.tasks.push({
                name: this.current,
                isDone: false
            })
            this.current = ''
        },
        complete(task) {
            this.tasks = this.tasks.map(t => {
                if (t.name === task.name) {
                    return { ...t, isDone: !t.isDone }
                }
                return { ...t }
            })
        },
        remove(task) {
            this.tasks = this.tasks.filter(t => t !== task)
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