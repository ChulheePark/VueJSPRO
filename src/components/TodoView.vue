<template>
  <div calss="todo-view">
     <section  @click="$emit('edit-change')">{{ titles }} <i class="editBtn fa fa-edit" aria-hidden="true"></i></section>
  </div>
</template>

<script>
export default {
    name: 'todo-view',
    props: ['titles']
}
</script>

<style>

</style>