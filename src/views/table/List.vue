<template>
  <div class="page-etl">
    <div class="page-button">
      <el-button type="primary" size="mini" @click="$router.push('/table/edit')">New</el-button>
    </div>

    <div class="page-title">
      Tables
    </div>
    <el-table
      :data="tableList"
      style="width: 100%"
    >
      <el-table-column
        prop="id"
        label="#"
        width="80"
      />
      <el-table-column
        prop="sourceDatabase"
        label="Source DB"
      />
      <el-table-column
        prop="sourceTable"
        label="Source Table"
      />
      <el-table-column
        prop="targetTable"
        label="Target Table"
      />
      <el-table-column
        prop="createTime"
        label="Create Time"
      />
      <el-table-column
        label="Operations"
        width="120"
      >
        <template slot-scope="scope">
          <el-button type="text" size="mini" @click="editTable(scope.row)">Edit</el-button>
          <el-button type="text" size="mini">Delete</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<style lang="scss">
.page-etl {
  .page-title {
    font-size: 14px;
    line-height: 28px;
    font-weight: bold;
    margin-bottom: 20px;
  }

  .page-button {
    float: right;
  }
}
</style>

<script>
import * as _ from 'lodash'
import { mapState } from 'vuex'

export default {
  name: 'TableList',

  computed: {
    ...mapState('table', [
      'tableList',
    ]),
  },

  mounted () {
    this.$store.dispatch('table/fetchTableList')
  },

  methods: {
    editTable (table) {
      this.$router.push({
        path: '/table/edit',
        query: _.pick(table, ['id'])
      })
    }
  }
}
</script>
