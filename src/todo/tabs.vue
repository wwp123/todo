<template>
  <div class="helper">
    <span class="left">{{unFinishedTodoLength}} items left</span>
    <div class="tabs">
      <span
        v-for="statu in status"
        :key="statu"
        :class="['statu', filter === statu ? 'actived' : '']"
        @click="toggleFilter(statu)"
      >
      {{statu}}</span>
    </div>
    <span class="right" @click="clearAllCompleted">Clear completed</span>
  </div>
</template>

<script>
export default {
  props: {
    filter: {
      type: String,
      required: true
    },
    todos: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      status: ['all','active','completed']
    }
  },
  computed:{
    unFinishedTodoLength() {
      return this.todos.filter(todo => !todo.completed).length
    }
  },
  methods: {
    toggleFilter(statu) {
      this.$emit('toggle', statu)
    },
    clearAllCompleted() {
      this.$emit('clearAllCompleted')
    }
  }
}
</script>

<style lang="stylus" scoped>
.helper {
  font-weight 100
  display flex
  justify-content space-between
  padding 5px 0
  line-height 30px
  background-color #fff
  font-size 14px
  font-smoothing antialiased
}
.left, .right, .tabs {
  padding 0 10px
  box-sizing border-box
}
.left, .right {
  width 150px
}
  .left {
    text-align left 
  }
  .right {
    text-align right 
    cursor pointer
  }
  .tabs {
    width 200px
    display flex
    justify-content space-around
    * {
      display inline-block
      padding 0 10px
      cursor pointer
      border 1px solid rgba(175,47,47,0)
      &.actived {
        border-color rgba(175,47,47,.4)
        border-radius 5px
      }
    }
  }
</style>
