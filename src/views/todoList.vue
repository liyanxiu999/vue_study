<template>
  <div class="todo_content">
    <h3>To Do List</h3>
    <div class="todo_input">
      <input type="text"
              placeholder="请输入内容"
              v-model="input"
              class="input">
      <button class="btn" @click="addTo">确认</button>
    </div>
    <div class="todo_tab">
      <table cellspacing="0" cellpadding="0">
        <colgroup>
          <col width="20%" />
          <col width="40%" />
          <col width="40%" />
        </colgroup>
        <thead>
          <tr>
            <th>序号</th>
            <th>内容</th>
            <th>操作</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item,i) in todoData"
              :key = 'i'>
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
      flag: false,
      index: -1,
      todoData: [{
        todolist: '111'
      }]
    }
  },
  methods: {
    addTo () {
      if (this.todoData.some((item) => item.todolist === this.input)) {
        this.input = ''
        return false
      }
      if (this.input === '') {
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
      console.log(this.todoData[index])
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
      background-color: pink;
      line-height: 50px;
      text-align: center;
    }
    .todo_input {
      width: 100%;
      height: 48px;
      line-height: 40px;
      text-align: center;
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
        background-color:#add;
        border: none;
      }
    }
    .todo_tab {
      width: 100%;
      height: 500px;
      overflow-y: auto;
      table {
        width: 100%;
        thead tr th{
          // &:nth-child(1) {
          //   width: 20%;
          // }
          // &:nth-child(2) {
          //   width: 40%;
          // }
          // &:nth-child(3) {
          //   width: 40%;
          // }
        }
        td {
          text-align: center;
        }
      }
    }
  }
</style>
