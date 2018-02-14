<template>
  <div class="todo-edit">
     <input type="text" class="input" v-model="edittitles" v-on:keyup.enter="procsave">
     <i class="editBtn fa fa-edit" aria-hidden="true" @click.prevent="procsave"></i>
     <i class="editBtn fa fa-reply-all" aria-hidden="true" @click="$emit('edit-redo')"></i>
  </div>
</template>

<script>
export default {
    name: 'todo-edit',
     props: ['titles'],
     data: () => {
         return {
             edittitles: '',
             orgtitles: ''
         }
     },
     mounted(){
         this.edittitles = this.titles;
         this.orgtitles = this.titles;
     },
     methods: {
         procsave() {
             this.$emit('update-change', this.orgtitles, this.edittitles);
             this.$emit('edit-redo');
         }
     }
}
</script>

<style>

</style>
