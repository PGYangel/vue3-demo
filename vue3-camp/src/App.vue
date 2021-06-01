<template>
  <div>
    <h1>{{ count }}</h1>
    <button @click="add">click</button>
    <hr />
    <h1>{{ state.val }}</h1>
    <input type="text" v-model="state.val" @keyup.enter="addTodo" />
    <ul>
      <li v-for="(todo, index) in state.todos" :key="index">{{ todo.name }}</li>
    </ul>
    <h1>total:{{ total }}</h1>
  </div>
</template>

<script>
// composition api
// ref是将简单数据结构变成响应式
// reactive是将复杂数据结构变成响应式
// unref可以将复杂数据结构进行展开输出
import { ref, reactive, computed } from "vue";
export default {
  name: "App",
  setup() {
    let count = ref(1);
    function add() {
      count.value++;
    }

    let state = reactive({
      todos: [
        { name: "啦啦啦", done: false },
        { name: "哈哈哈", done: false },
      ],
      val: "",
    });
    let total = computed(() => state.todos.length);

    function addTodo() {
      state.todos.push({
        done: false,
        name: state.val,
      });
      state.val = "";
    }

    //使用unref展开输出，这样在上面引用就不需要加state前缀
    // return {...unref(state)}
    return { count, add, state, total, addTodo };
  },
};
</script>
