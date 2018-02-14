<template>
  <section>
      <transition-group name="list" tag="ul">
          <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
              <i class="checkBtn fa fa-check" aria-hidden="true"></i>
              <template>
                <component :is="vuechange(todoItem)" 
                  v-bind:titles="todoItem" 
                  v-on:edit-change="activenames=todoItem"
                  v-on:edit-redo="activenames=''"
                  v-on:update-change="updatedsaves">
                </component>
              </template>
              <span class="removeBtn" type="button">                  
                  <i class="fa fa-trash-o" aria-hidden="true"  @click="removeTodo(todoItem, index)"></i>
              </span>
          </li>        
      </transition-group>
  </section>
</template>

<script>
import TodoEdit from './TodoEdit'
import TodoView from './TodoView'

export default {
  data() {
      return {
          checkidx: false,
          activenames: null
      }
  },
  props:['propsdata'],
  components: {
      TodoEdit, TodoView
  },
  methods: {
      removeTodo(todoItem, index) {
      this.$emit('removeTodo', todoItem, index);          
      },
      vuechange(activenames2){
        return this.activenames && this.activenames === activenames2 ? 'todo-edit' : 'todo-view';      
      },
      updatedsaves(to01, to02){
         if(to01 != to02){
         alert('변경');
         //localStorage.removeItem(to01);        
         //localStorage.setItem(to02, to02);
          //this.todoItems.push(to02);        
        }
        
      }
  }
}
</script>

<style>
ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}

li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}

.checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}

.removeBtn {
    margin-left: auto;
    color: #de4343;
}

.editBtn {
    margin-left: auto;
    color: #0409f8;
}

.list-item {
    display: inline-block;
    margin-right: 10px;
}

.list-move {
    transition: transform 1s;
}

.list-enter-active, .list-leave-active {
    transition: all 1s;
}

.list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
}
</style>
