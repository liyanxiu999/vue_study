<template>
  <div class="todo_content">
    <h3>To Do List</h3>
    <div class="todo_input">
      <el-input v-model="input" placeholder="请输入内容" class="input"></el-input>
      <el-button type="primary" @click="addTo">添加</el-button>
    </div>
    <template>
    <el-table
      :data="todoData"
      style="width: 100%">
      <el-table-column
        type="index"
        label="序号"
        width="100"
        align="center">
      </el-table-column>
      <el-table-column
        prop="todolist"
        label="内容"
        width="180"
        align="center">
      </el-table-column>
      <el-table-column
        label="操作"
        align="center">
        <template slot-scope="scope">
        <el-button
          size="mini"
          @click="handleEdit(scope.$index, scope.row)">编辑</el-button>
        <el-button
          size="mini"
          type="danger"
          @click="handleDelete(scope.$index, scope.row)">删除</el-button>
      </template>
      </el-table-column>
    </el-table>
  </template>
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
      if (this.input === '') {
        this.$message({
          message: '当前内容为空',
          type: 'warning'
        })
        return false
      }
      if (this.todoData.some((item) => item.todolist === this.input)) {
        this.$message.error('当前内容已存在')
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
      this.$message({
        message: '恭喜你，添加成功',
        type: 'success'
      })
    },
    handleEdit (index, row) {
      this.input = row.todolist
      this.index = index
      this.flag = true
    },
    handleDelete (index, row) {
      this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        this.todoData.splice(index, 1)
        this.$message({
          type: 'success',
          message: '删除成功!'
        })
      }).catch(() => {
        this.$message({
          type: 'info',
          message: '已取消删除'
        })
      })
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
      }
    }
  }
</style>
