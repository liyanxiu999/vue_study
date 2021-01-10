<template>
  <div class="todo_content">
    <h3>To Do List</h3>
    <div class="todo_input">
      <input type="text" placeholder="请输入内容
      " class="input" v-model="input">
      <button class="btn" @click="addTo">确认</button>
    </div>
    <div class="todo_tab">
      <table cellspacing='0' cellpadding='0'>
        <thead>
          <colgroup>
            <col width='20%'>
            <col width='40%'>
            <col width='40%'>
          </colgroup>
          <tr>
            <th>序号</th>
            <th>内容</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item,i) in todoData"
              :key="i">
            <td>{{i+1}}</td>
            <td>{{item.todolist}}</td>
            <td>
              <button @click="edit(i)">编辑</button>
              <button @click="delet(i)">删除</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
export default {
  data () {
    return {
      input: '',
      index: -1,
      flag: false,
      todoData: [{
        todolist: '111'
      }]
    }
  },
  methods: {
    addTo () {
      if (this.input === '') {
        return false
      }
      if (this.todoData.some((item) => item.todolist === this.input)) {
        this.input = ''
        return false
      }
      if (!this.flag) {
        this.todoData.push({
          todolist: this.input
        })
      } else {
        this.todoData.splice(this.index, 1, {
          todolist: this.input
        })
        this.flag = false
      }
      this.input = ''
    },
    edit (index) {
      this.input = this.todoData[index].todolist
      this.index = index
      this.flag = true
    },
    delet (index) {
      this.todoData.splice(index, 1)
    }
  }
}
</script>
<style lang="less">
  .todo_content {
    width: 500px;
    height: 600px;
    border: 1px solid;
    h3 {
      width: 100%;
      height: 50px;
      background-color: cyan;
      text-align: center;
      line-height: 50px;
    }
    .todo_input {
      width: 100%;
      height: 50px;
      text-align: center;
      line-height: 50px;
      .input {
        width: 300px;
        height: 40px;
        margin: 4px;
        border: 1px solid cyan;
      }
      .btn {
        width: 40px;
        height: 40px;
        line-height: 10px;
        text-align: center;
        border: none;
        background-color: cyan;
      }
    }
    .todo_tab {
      width: 100%;
      height: 500px;
      table {
        width: 100%;
        td {
          text-align: center;
          button {
            background-color: cyan;
            border: none;
          }
        }
      }
    }
  }
</style>
