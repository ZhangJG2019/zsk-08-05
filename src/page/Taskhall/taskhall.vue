<template>
  <!-- <div class="checkout"> -->
  <div class="taskhall">
    <y-header>
      <div slot="nav"></div>
    </y-header>

    <el-card class="box-card w1200">
      <div class="tablecontent">
        <!-- 表格展示 1 -->
        <el-table
          :data="
            tableData.slice(
              (currentPage - 1) * pagesize,
              currentPage * pagesize
            )
          "
          border
          stripe
          style="width: 100%"
          highlight-current-row
          @current-change="handleCurrentChange"
          align="center"
        >
          <el-table-column type="selection" width="55" align="center">
          </el-table-column>
          <!-- 自增主键 -->
          <el-table-column
            prop="id"
            label="自增主键"
            v-if="(show = false)"
            width="150"
            align="center"
          >
          </el-table-column>
          <!-- 词条主键 -->
          <el-table-column
            prop="projectId"
            label="词条主键"
            width="150"
            align="center"
            v-if="(show = false)"
          >
          </el-table-column>
          <!-- 子任务分类主键 -->
          <el-table-column
            prop="subCategoryId"
            label="子任务分类主键"
            width="150"
            align="center"
            v-if="(show = false)"
          >
          </el-table-column>
          <!-- 任务操作内容类型（project、disease、gene、genePor、drug） 显-->
          <el-table-column
            prop="contentType"
            label="任务操作内容类型"
            width="150"
            align="center"
          >
          </el-table-column>
          <!-- 任务对象主键 -->
          <el-table-column
            prop="targetId"
            label="任务对象主键"
            width="150"
            align="center"
            v-if="(show = false)"
          >
          </el-table-column>
          <!-- 任务名称 显-->
          <el-table-column
            fixed
            prop="name"
            label="任务名称"
            width="150"
            align="center"
          >
          </el-table-column>
          <!-- 开始时间 -->
          <el-table-column
            id="startTime"
            prop="startTime"
            label="开始时间"
            align="center"
            sortable
            :default-sort="{ prop: 'date', order: 'descending' }"
            v-if="(show = false)"
            width="180"
          >
            <i class="el-icon-time"></i>
          </el-table-column>
          <!-- 结束时间 显-->
          <el-table-column
            id="endTime"
            prop="endTime"
            label="结束时间"
            align="center"
            sortable
            :default-sort="{ prop: 'date', order: 'descending' }"
            width="180"
          >
            <i class="el-icon-time"></i>
          </el-table-column>
          <!-- 任务创建者 -->
          <el-table-column
            prop="creator"
            label="任务创建者"
            width="120"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
          <!-- 标注员 -->
          <el-table-column
            prop="commonUser"
            label="标注员"
            width="120"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
          <!-- 检查员 -->
          <el-table-column
            prop="inspector"
            label="检查员"
            width="120"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
          <!-- 质检员 -->
          <el-table-column
            prop="editor"
            label="质检员"
            width="120"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
          <!-- 专家 -->
          <el-table-column
            prop="expert"
            label="专家"
            width="120"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
          <!-- 创建时间 -->
          <el-table-column
            id="createTime"
            prop="createTime"
            label="创建时间"
            align="center"
            sortable
            :default-sort="{ prop: 'date', order: 'descending' }"
            v-if="(show = false)"
            width="180"
          >
            <i class="el-icon-time"></i>
          </el-table-column>
          <!-- 标注员完成时间 -->
          <el-table-column
            id="commonTime"
            prop="commonTime"
            label="标注员完成时间"
            align="center"
            sortable
            :default-sort="{ prop: 'date', order: 'descending' }"
            width="180"
            v-if="(show = false)"
          >
            <i class="el-icon-time"></i>
          </el-table-column>
          <!-- 检查员完成时间 -->
          <el-table-column
            id="inspectorTime"
            prop="inspectorTime"
            label="检查员完成时间"
            align="center"
            sortable
            :default-sort="{ prop: 'date', order: 'descending' }"
            width="180"
            v-if="(show = false)"
          >
            <i class="el-icon-time"></i>
          </el-table-column>
          <!-- 质检员完成时间 -->
          <el-table-column
            id="editTime"
            prop="editTime"
            label="质检员完成时间"
            align="center"
            sortable
            :default-sort="{ prop: 'date', order: 'descending' }"
            width="180"
            v-if="(show = false)"
          >
            <i class="el-icon-time"></i>
          </el-table-column>
          <!-- 专家完成时间 -->
          <el-table-column
            id="expertTime"
            prop="expertTime"
            label="专家完成时间"
            align="center"
            sortable
            :default-sort="{ prop: 'date', order: 'descending' }"
            width="180"
            v-if="(show = false)"
          >
            <i class="el-icon-time"></i>
          </el-table-column>
          <!-- 任务类型(create/update) -->
          <el-table-column
            prop="type"
            label="任务类型"
            width="100"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
          <!-- 任务状态 显-->
          <el-table-column
            prop="flag"
            label="任务状态"
            width="150"
            align="center"
          >
          </el-table-column>
          <!-- 模板主键 -->
          <el-table-column
            prop="commentId"
            label="模板主键"
            width="150"
            align="center"
            v-if="(show = false)"
          >
          </el-table-column>
          <!-- 版本号 显-->
          <el-table-column
            prop="version"
            label="版本号"
            width="100"
            align="center"
          >
          </el-table-column>
          <!-- 操作 显-->
          <el-table-column
            label="操作"
            align="center"
            fixed="right"
            width="130"
          >
            <template slot-scope="scope">
              <el-button @click="showIframe(scope.row)" type="text" size="small"
                >领取任务</el-button
              >
            </template>
          </el-table-column>
          <!-- 任务创建者 显-->
          <el-table-column
            prop="createrName"
            label="任务创建者"
            width="120"
            align="center"
          >
          </el-table-column>
          <!-- 标注员 显-->
          <el-table-column
            prop="commonUserName"
            label="标注员"
            width="100"
            align="center"
          >
          </el-table-column>
          <!-- 检查员 显-->
          <el-table-column
            prop="inspectorName"
            label="检查员"
            width="100"
            align="center"
          >
          </el-table-column>
          <!-- 质检员 显-->
          <el-table-column
            prop="editorName"
            label="质检员"
            width="100"
            align="center"
          >
          </el-table-column>
          <!-- 专家 显-->
          <el-table-column
            prop="expertName"
            label="专家"
            width="100"
            align="center"
          >
          </el-table-column>
          <!-- 二级菜单名称 -->
          <el-table-column
            prop="subCategoryName"
            label="二级菜单名称"
            width="100"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
          <!-- 词条名称 -->
          <el-table-column
            prop="targetName"
            label="词条名称"
            width="100"
            v-if="(show = false)"
            align="center"
          >
          </el-table-column>
        </el-table>
        <!-- 表格展示 2 -->
        <!-- 分页 1 -->
        <div class="fenye">
          <el-pagination
            @current-change="handleCurrentChanges"
            background
            layout="prev, pager, next"
            :total="tableData.length"
            align="center"
          >
          </el-pagination>
        </div>
        <!-- 分页 2 -->
      </div>
    </el-card>

    <y-footer></y-footer>

    <iframe
      v-show="iframeState"
      id="show-iframe"
      frameborder="0"
      name="showHere"
      scrolling="auto"
      src=""
    ></iframe>
    <iframe
      id="dialogFrame"
      frameborder="0"
      scrolling="no"
      style="background-color:transparent; position: absolute; z-index: -1; width: 100%; height: 100%; top: 0;left:0;"
    ></iframe>
  </div>
</template>
<script>
import YShelf from '/components/shelf'
import YButton from '/components/YButton'
import YPopup from '/components/popup'
import YHeader from '/common/header'
import YFooter from '/common/footer'
import $ from 'jquery'
import 'element-ui'
export default {
  name: 'hello',
  data() {
    return {
      outerVisible: false,
      innerVisible: false,
      currentPage: 1, // 初始页
      pagesize: 10, //    每页的数据
      tableData: [
        {
          id: '1',
          name: '药物基因用药建议的给出-词条001',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:11',
          createrName: 'administrator',
          commonUserName: '111',
          inspector: '222',
          qualityinspector: '333',
          experts: '444',
          taskType: '修改',
          flag: '检查员可领取',
          version: '1'
        },
        {
          id: '2',
          name: '药物基因用药建议的给出-词条002',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:12',
          createrName: '55',
          commonUserName: '666',
          inspector: '77',
          qualityinspector: '88',
          experts: '99',
          taskType: '修改',
          flag: '完成',
          version: '1'
        },
        {
          id: '3',
          name: '药物基因用药建议的给出-词条003',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:10',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '检查员可领取',
          version: '1'
        },
        {
          id: '4',
          name: '药物基因用药建议的给出-词条004',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:01',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '专家可领取',
          version: '1'
        },
        {
          id: '5',
          name: '药物基因用药建议的给出-词条005',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:04',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '完成',
          version: '1'
        },
        {
          id: '6',
          name: '药物基因用药建议的给出-词条006',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:02',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '完成',
          version: '1'
        },
        {
          id: '7',
          name: '药物基因用药建议的给出-词条007',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:03',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '专家可领取',
          version: '1'
        },
        {
          id: '8',
          name: '药物基因用药建议的给出-词条008',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:06',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '标注员可领取',
          version: '1'
        },
        {
          id: '9',
          name: '药物基因用药建议的给出-词条009',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:15',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '专家可领取',
          version: '1'
        },
        {
          id: '10',
          name: '药物基因用药建议的给出-词条010',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:25',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '标注员可领取',
          version: '1'
        },
        {
          id: '11',
          name: '药物基因用药建议的给出-词条011',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:35',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '专家可领取',
          version: '1'
        },
        {
          id: '12',
          name: '药物基因用药建议的给出-词条012',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:45',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '标注员可领取',
          version: '1'
        },
        {
          id: '13',
          name: '药物基因用药建议的给出-词条013',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:55',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '专家可领取',
          version: '1'
        },
        {
          id: '14',
          name: '药物基因用药建议的给出-词条014',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:17',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '标注员可领取',
          version: '1'
        },
        {
          id: '15',
          name: '药物基因用药建议的给出-词条015',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:27',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '标注员可领取',
          version: '1'
        },
        {
          id: '16',
          name: '药物基因用药建议的给出-词条016',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:37',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '专家可领取',
          version: '1'
        },
        {
          id: '17',
          name: '药物基因用药建议的给出-词条017',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:16',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '质检员可领取',
          version: '1'
        },
        {
          id: '18',
          name: '药物基因用药建议的给出-词条018',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:26',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '标注员可领取',
          version: '1'
        },
        {
          id: '19',
          name: '药物基因用药建议的给出-词条019',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:36',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '修改',
          flag: '标注员可领取',
          version: '1'
        },
        {
          id: '20',
          name: '药物基因用药建议的给出-词条020',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:46',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '质检员可领取',
          version: '1'
        },
        {
          id: '21',
          name: '药物基因用药建议的给出-词条021',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:56',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '质检员可领取',
          version: '1'
        },
        {
          id: '22',
          name: '药物基因用药建议的给出-词条022',
          startTime: '2019-07-10 21:16:05',
          endTime: '2019-07-11 20:16:55',
          createrName: 'administrator',
          commonUserName: 'administrator',
          inspector: 'administrator',
          qualityinspector: 'administrator',
          experts: 'administrator',
          taskType: '新建',
          flag: '专家可领取',
          version: '1'
        }
      ],
      iframeState: false,
      goBackState: false,
      webAddress: [
        {
          name: 'segmentFault',
          link: 'https://segmentfault.com/a/1190000004502619'
        },
        {
          name: '博客',
          link: 'http://vuex.vuejs.org/'
        },
        {
          name: '特效',
          link: 'http://www.yyyweb.com/377.html'
        }
      ]
    }
  },
  mounted() {
    // 点击首页跳转页面 1
    $('.index').click(function() {
      $('a', this)[0].click()
    })
    // 点击首页跳转页面 2
    // 通过iframe领取任务 1
    const oIframe = document.getElementById('show-iframe')
    const deviceWidth = document.documentElement.clientWidth
    const deviceHeight = document.documentElement.clientHeight
    oIframe.style.width = deviceWidth + 'px'
    oIframe.style.height = deviceHeight + 'px'
    // 通过iframe领取任务 2
  },
  methods: {
    // iframe弹窗
    goBack() {
      this.goBackState = false
      this.iframeState = false
    },
    showIframe(a) {
      console.log(a)
      this.goBackState = true
      this.iframeState = true
    },
    // 切换页面
    handleCurrentChange(val) {
      this.currentRow = val
    },
    handleCurrentChanges: function(currentPage) {
      this.currentPage = currentPage
      console.log(this.currentPage) // 点击第几页
    }
  },
  components: {
    YShelf,
    YButton,
    YPopup,
    YHeader,
    YFooter
  }
}
</script>
<style lang="scss" rel="stylesheet/scss" scoped>
</style>
