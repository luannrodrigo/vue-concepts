<template>
    <div>
        <h1 v-bind:style="{textDecoration: decoration}"> hello world {{ name }}</h1>
        <input type="text" v-model="name" />
    </div>
</template>

<script>
export default {
    data: () => ({
        name: 'luann',
        decoration: 'underline'
    })
}
</script>

<style>

</style>