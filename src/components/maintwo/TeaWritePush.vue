<template>
<!-- 最优推送 -->
    <div class="inputTable">
        <!-- 表格内容 -->
        <div class="containerClass">
            <div class="maincm">
                <div class="left">
                    <span>班级:</span>
                    <el-select v-model="value" placeholder="请选择">
                        <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
                        </el-option>
                    </el-select>

                    <span>学生姓名：</span>
                    <input type="text" name="search" placeholder="支持模糊查询">

                    <span>作业任务：</span>
                    <input type="text" name="search" placeholder="支持模糊查询">
                </div>
                <div class="right flex-between">
                    <button>查询</button>
                </div>
            </div>

            <table>
                <thead>
                    <tr>
                        <th></th>
                        <th>序号</th>
                        <th>班级</th>
                        <th>学生</th>
                        <th>作业任务</th>
                        <th>推送时间</th>
                        <th>推送资料</th>
                        <th style="width: 25%">操作</th>
                    </tr>
                </thead>

                <tbody>
                    <tr>
                        <td>
                            <el-checkbox></el-checkbox>
                        </td>
                        <td>1</td>
                        <td>class02</td>
                        <td>张三</td>
                        <td>实训报告一</td>
                        <td>2017-04-05 12:12:12</td>
                        <td>实训报告.xls</td>
                        <td>
                            <button>下载</button>
                            <button>取消推送</button>
                        </td>
                    </tr>
                    <tr>
                        <td>
                            <el-checkbox></el-checkbox>
                        </td>
                        <td>2</td>
                        <td>class02</td>
                        <td>张三</td>
                        <td>实训报告一</td>
                        <td>2017-04-05 12:12:12</td>
                        <td>实训报告.xls</td>
                        <td>
                            <button>下载</button>
                            <button>取消推送</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
        <!-- table end -->
    </div>
</template>

<script>
export default {
    data() {
        return {
            breadcrumb: [
                { name: "首页", to: "/" },
                { name: "写作平台", to: "/teawritemain" },
                { name: "最优推送", to: "" }
            ],

            options: [
                {
                    value: "选项1",
                    label: "class01"
                },
                {
                    value: "选项2",
                    label: "class02"
                }
            ],

            value: ""
        };
    },

    mounted() {
        this.$emit("getData", this.breadcrumb);
    }
};
</script>

<style scoped>
.containerClass {
    min-width: 670px;
    margin: 5px 0px;
}

.maincm {
    display: flex;
    justify-content: space-between;
}

.left input {
    width: 230px;
    height: 42px;
    border-radius: 5px;
    border: 1px solid #cdcdcd;
}

.right button {
    width: 120px;
    height: 42px;
    color: #fff;
    background-image: url("../../../static/images/classmanage/bluebutton.png");
    background-size: 100% 100%;
    border: none;
    margin-left: 10px;
}

table {
    border: 1px solid #bbe0fb;
    width: 100%;
    margin-top: 20px;
    background-color: #f7fbfe;
}

table td {
    text-align: center;
    border: 1px solid #bbe0fb;
}

span{
    margin: 0px 10px;
}
</style>


