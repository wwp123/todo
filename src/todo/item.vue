<template>
  <div :class="['todo-item', todo.completed ? 'completed' : '']">
    <input 
      type="checkbox"
      class="toggle"
      v-model="todo.completed"
    >
    <label>{{todo.content}}</label>
    <button class="destory" @click="deleteTodo"></button>
  </div>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    deleteTodo() {
      this.$emit('del', this.todo.id)
    }
  }
}
</script>

<style lang="stylus" scoped>
  .todo-item {
    position relative
    background-color #fff
    font-size 24px
    border-bottom 1px solid rgba(0,0,0,.06)
    &:hover {
      .destory:after {
        content '×'
      }
    } 
    label {
      white-space pre-line
      word-break break-all
      padding 15px 60px 15px 15px
      margin-left 45px
      display block
      line-height 1.2
      transition color 0.4s
    }
    &.completed {
      label {
        color #d9d9d9
        text-decoration line-through
      }
    }
  }
  .toggle {
    text-align center
    width 30px
    height 30px
    position absolute
    top 0
    bottom 0
    left 15px
    margin auto 0
    border 1px solid #ccc
    border-radius 50% 
    appearance none
    outline none
    cursor pointer
    text-align center
    line-height 30px
    font-size 20px
    &:checked:after {
      content '√'
      color #5da708
    }
  }
  .destory {
    position absolute
    top 0
    bottom 0
    right 10px
    width 40px
    height 40px
    margin auto 0 11px
    font-size 30px
    color #cc9a9a
    transition color 0.2s ease-out
    background-color transparent
    appearance none
    border-width 0
    cursor pointer
    outline none
  }
</style>
