<template>
  <div>
    <!-- 这是听一听页面 -->
    <div class="flex-between">
      <div class="flex-start">
        <div class="flex-start">
          <div>
            <span class="nowrap">班级名称</span>
          </div>
          <div class="ting1">
            <el-select v-model="valClass" @change="getList()">
              <el-option v-for="item in getClassList" :key="item.value" :label="item.label" :value="item.value">
              </el-option>
            </el-select>
          </div>
        </div>
        <!-- <div class="flex-start ting1">
          <div>
            <span class="nowrap">内容模块</span>
          </div>
          <div class="ting1">
            <el-select></el-select>
          </div>
        </div> -->
      </div>

      <div class="btn-lan nowrap">
        <button @click="setTableData()">保存</button>
        <button>课程重置</button>
        <button>全部课程重置</button>
      </div>
    </div>
    <div style="marginTop:10px;">
      <table class="table1">
        <thead>
          <tr>
            <th>关卡模块</th>
            <th>场景模块</th>
            <th colspan="2">关卡名称</th>
            <th colspan="2">快卡启用</th>
            <th colspan="2">答案设置</th>
            <th>分值设定(单位:%)</th>
          </tr>
          <tr>
            <th></th>
            <th></th>
            <th class="btn-lv">
              <button @click="setAllVal(true)">全选择</button>
            </th>
            <th class="btn-lv">
              <button @click="setAllVal(false)">全取消</button>
            </th>
            <th class="btn-lv">
              <button @click="setAllTaskOpened('1')">全开放</button>
            </th>
            <th class="btn-lv">
              <button @click="setAllTaskOpened('0')">全关闭</button>
            </th>
            <th class="btn-lv">
              <button @click="setAllAnswerOpened('1')">全开放</button>
            </th>
            <th class="btn-lv">
              <button @click="setAllAnswerOpened('0')">全关闭</button>
            </th>
            <th></th>
          </tr>

        </thead>
        <tbody v-if="isTableData">
          <tr>
            <td colspan="9" class="tishi">
              请选择正确的班级后查询
            </td>
          </tr>
        </tbody>
        <tbody v-else>
          <tr v-for="(item,index) in tableData[2]" :key="index">
            <!-- <td :rowspan="tableData[1][index].count" v-if="tableData[1]&&tableData[1][index].count!==0">{{tableData[1][index].menu.menuName}}</td> -->
            <td :rowspan="tableData[2][index].count" v-if="tableData[2]&&tableData[2][index].count!==0">{{tableData[2][index].menu.menuName}}</td>
            <td :rowspan="tableData[3][index].count" v-if="tableData[3]&&tableData[3][index].count!==0">{{tableData[3][index].menu.menuName}}</td>
            <td colspan="2" v-if="tableData[4]&&tableData[4][index].count!==0">
              <div style="text-align:left;margin:0 auto;max-width:120px;">
                <el-checkbox v-model="tableData[4][index].value">
                  {{tableData[4][index].menu.menuName}}
                </el-checkbox>
              </div>
            </td>
            <td v-if="tableData[4]&&tableData[4][index].count!==0">
              <div>
                <el-radio v-model="tableData[4][index].set.taskOpened" label="1">开放</el-radio>
              </div>
            </td>
            <td v-if="tableData[4]&&tableData[4][index].count!==0">
              <div>
                <el-radio v-model="tableData[4][index].set.taskOpened" label="0">关闭</el-radio>
              </div>
            </td>
            <td v-if="tableData[4]&&tableData[4][index].count!==0">
              <div>
                <el-radio v-model="tableData[4][index].set.answerOpened" label="1">开放</el-radio>

              </div>
            </td>
            <td v-if="tableData[4]&&tableData[4][index].count!==0">
              <div>
                <el-radio v-model="tableData[4][index].set.answerOpened" label="0">关闭</el-radio>

              </div>
            </td>
            <td v-if="tableData[4]&&tableData[4][index].count!==0">
              <div style="padding:0 10px;">
                <el-select v-model="tableData[4][index].setDetail.resultRatio">
                  <el-option v-for="item in getQuanzhong" :key="item" :label="item" :value="item">
                  </el-option>
                </el-select>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>
<script>
import { mapGetters } from "vuex";
import getData from "../public/setTableData";
export default {
    name: "TeaSpeTing",
    data() {
        return {
            valClass: "请选择班级",
            tableData: [],
            breadcrumb: [
                { name: "首页", to: "/" },
                { name: "口语平台", to: "/teaspe" },
                { name: "听一听", to: "" }
            ],
            tabs: [
                { name: "听一听", to: "/teaspeting" },
                { name: "说一说", to: "/teaspeshuo" },
                { name: "能力测评设置", to: "/teaspenlcp" },
                { name: "成绩权重设置", to: "/teaspecjqz" }
            ]
        };
    },
    computed: {
        ...mapGetters(["getUser", "getClassList", "getQuanzhong"]),
        isTableData() {
            if (this.tableData.length === 0) {
                return true;
            } else {
                return false;
            }
        }
    },
    methods: {
        // 设置答案全开放
        setAllAnswerOpened(str) {
            let tableData = this.tableData;
            tableData[4].map((val, i, arr) => {
                arr[i].set.answerOpened = str;
            });
        },
        // 设置关卡启用全开放
        setAllTaskOpened(str) {
            let tableData = this.tableData;
            tableData[4].map((val, i, arr) => {
                arr[i].set.taskOpened = str;
            });
        },
        // 设置关卡名称全选择
        setAllVal(str) {
            let tableData = this.tableData;
            tableData[4].map((val, i, arr) => {
                arr[i].value = str;
            });
        },
        // 保存事件
        setTableData() {
            // 判断总分觉得是否提交
            let isToHttp = true;
            let tableData = this.tableData;
            if (tableData[4]) {
                let newData = tableData[3]
                    .filter(val => {
                        return val.count !== 0;
                    })
                    .map(val => {
                        let zongfen = 0;
                        val.list.map(val => {
                            zongfen += parseFloat(val.setDetail.resultRatio);
                        });
                        // 判断总分是否满足100%
                        if (zongfen < 100) {
                            isToHttp = false;
                        }
                    });
                let settableData = tableData[4].map(val => {
                    if (val.value === true) {
                        let setData = {
                            xueid: val.set.xueid,
                            teaId: val.set.teaId,
                            classId: val.set.classId,
                            taskOpened: val.set.taskOpened,
                            answerOpened: val.set.answerOpened,
                            subtitleOpened: val.set.subtitleOpened,
                            menuNo: val.set.menuNo,
                            updatedUserId: this.getUser.userid
                        };
                        return setData;
                    }
                });

                let resultRatio = tableData[4].map(val => {
                    if (val.value === true) {
                        let setData = {
                            xueid: val.setDetail.xueid,
                            scoreSetId: val.setDetail.scoreSetId,
                            menuNo: val.setDetail.menuNo,
                            resultRatio: val.setDetail.resultRatio,
                            updatedUserId: this.getUser.userid
                        };
                        return setData;
                    }
                });
                settableData = settableData.filter(val => {
                    return val !== undefined;
                });
                resultRatio = resultRatio.filter(val => {
                    return val !== undefined;
                });
                if (isToHttp) {
                    if (settableData.length > 0 && resultRatio.length > 0) {
                        resultRatio.map(val => {
                            val.resultRatio = val.resultRatio.replace("%", "");
                        });
                        console.log(resultRatio);
                        this.$axios
                            .post("busjapspe/tea/set/set/editSet", {
                                set: JSON.stringify(settableData),
                                setDetail: JSON.stringify(resultRatio)
                            })
                            .then(res => {
                                console.log(res);
                            });
                    } else {
                        this.$message({
                            message: "请在要修改的关卡前打钩",
                            type: "warning"
                        });
                    }
                } else {
                    this.$message({
                        message: "模块的总分必须满足100%",
                        type: "warning"
                    });
                }
            } else {
                this.$message({
                    message: "请先获取数据！",
                    type: "warning"
                });
            }
        },
        // 获取表格列表数据
        getList() {
            this.$axios
                .get("/busjapspe/tea/set/set/setList", {
                    // 听一听menuNo.2
                    menuNo: 2,
                    teaId: this.getUser.userid,
                    classId: this.valClass
                })
                .then(res => {
                    let data = getData(res.data.results);
                    data[4].map(val => {
                        val.value = false;
                        val.set = JSON.parse(val.set);
                        val.setDetail = JSON.parse(val.setDetail);
                    });
                    data[4].map(val => {
                        val.setDetail.resultRatio =
                            val.setDetail.resultRatio + "%";
                    });
                    this.tableData = data;
                    console.log(data);
                });
        }
    },
    created() {},
    mounted() {
        let tabs = this.tabs;
        let breadcrumb = this.breadcrumb;
        let n = 0;
        this.$emit("getData", { tabs, breadcrumb, n });
    }
};
</script>
<style scoped>
.ting1 {
    margin: 0 10px;
}
</style>