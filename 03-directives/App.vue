<template>
  <div>
    <h1>My task list</h1>
    <button @click="() => showList = !showList">Show list</button>
    <br />
    <input type="text" v-focus>
    <ul v-if="showList">
        <li 
            v-for="(task, index) in tasks"
            :key="`${task}-${index}`"
        >
            {{ task.name }}
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
    })
}
</script>

<style>

</style>