<template>
    <div class="contentMain">
        <div id="dataAll">
            <div class="data-left">
                 <router-link to="/home/all">数据总览</router-link>
            </div>
            <div class="data-right">
                <el-breadcrumb separator="">
                    <el-breadcrumb-item :to="{ path: '/home' }">首页<i class='el-icon-caret-right'></i></el-breadcrumb-item>
                          <!--此处渲染时间范围-->
                    <el-breadcrumb-item>{{timeValue}}<i class='el-icon-caret-right'></i></el-breadcrumb-item>
                    <el-breadcrumb-item>{{gameName}}</el-breadcrumb-item>
                   
                </el-breadcrumb>
                 <div class="tag">
                     <el-tag
                        v-for="tag in tags"
                        :closable="true"
                        :type="tag.type"
                        :key="tag"
                        :close-transition="false"
                        @close="tagClose(tag)"
                        >
                        {{tag.name}}
                        </el-tag>
                 </div>
                <div class="block">
    <!--时间选择器-->
                    <el-date-picker
                      v-model="value4"
                      type="daterange"
                      :picker-options="pickerOptions2"
                      :editable=false
                      placeholder="选择时间范围"
                      align="right"
                      style="width:200px">
                    </el-date-picker>
                </div>
                <!--筛选条件-->
                <el-button type="primary" @click="callfilter">筛选</el-button>
            </div>
        </div>
        <div id="menuAll">
            <div class="leftmenu">
                <!--<el-menu default-active="2" class="el-menu-vertical-demo" v-bind:router="true" @open="handleOpen" @close="handleClose">
                    <el-submenu index="player">
                        <template slot="title"><i class="el-icon-message"></i>游戏玩家</template>
<el-menu-item index="/home/NewPlayer">新增玩家</el-menu-item>
<el-menu-item index="/home/JumpPlayer">活跃玩家</el-menu-item>
<el-menu-item index="/home/AlivePlayer">玩家留存</el-menu-item>
<el-menu-item index="/home/PayPoint">付费转化</el-menu-item>
<el-menu-item index="/home/RemovePlayer">玩家流失</el-menu-item>
<el-menu-item index="/home/UserDevice">设备相关</el-menu-item>
</el-submenu>
<el-menu-item index="/home/OnlineExp"><i class="el-icon-menu"></i>在线分析</el-menu-item>
<el-menu-item index="/home/RmbPlayer"><i class="el-icon-edit"></i>大R用户</el-menu-item>
<el-submenu index="2">
    <template slot="title"><i class="el-icon-view"></i>等级分析</template>
    <el-menu-item index="/home/LevelInfo">等级详解</el-menu-item>
    <el-menu-item index="/home/LevelPlace">等级分布</el-menu-item>
    <el-menu-item index="/home/NewPlayerLevel">新玩家进度</el-menu-item>
</el-submenu>
<el-submenu index="3">
    <template slot="title"><i class="el-icon-document"></i>虚拟消费</template>
    <el-menu-item index="/home/VituralMoney">虚拟币</el-menu-item>
    <el-menu-item index="/home/ConsumerPreferences">消费喜好</el-menu-item>
    <el-menu-item index="/home/VituralPoint">消费点</el-menu-item>
</el-submenu>
<el-submenu index="4">
    <template slot="title"><i class="el-icon-upload2"></i>收入分析</template>
    <el-menu-item index="/home/GetMoneyData">收入数据</el-menu-item>
    <el-menu-item index="/home/PayData">付费渗透</el-menu-item>
    <el-menu-item index="/home/PlayerToMoney">新玩家价值</el-menu-item>
    <el-menu-item index="/home/PayWay">付费习惯</el-menu-item>
</el-submenu>
</el-menu>-->
<el-tree :data="data" :props="defaultProps" @node-click="handleNodeClick"></el-tree>


</div>
<div class="rightcontent">
    <transition enter-active-class="animated quick fadeIn" leave-active-class="animated quick fadeOut" mode="out-in">
        <router-view></router-view>
    </transition>

</div>
</div>


</div>
</template>

<script>
    export default {

        mounted() {
            // if (!(window.localStorage.getItem("anfanToken"))) {
            //     window.location.href = "/"
            // } else {

            // }
            var _this = this;
            //监听选择了游戏
            Event.$on("chooseGame", function(game) {
                _this.gameName = game;

            })

            //监听选择的区服 渲染tag标签
            Event.$on("pushChoose", function(data) {
                _this.tags = [];

                for (var i = 0; i < data.length; i++) {
                    _this.tags.push({
                        name: data[i]
                    })

                }

            })

            this.$watch('value4', function() {
                //执行其他代码
                this.timeValue = (new Date(this.value4[0])).toLocaleDateString() + '-' + (new Date(this.value4[1])).toLocaleDateString()
            })

        },
        data() {
            return {
                data: [{
                    label: '游戏玩家',
                    children: [{
                        label: '新增玩家'
                    }, {
                        label: '活跃玩家'
                    }, {
                        label: '玩家留存'
                    }, {
                        label: '付费转化'
                    }, {
                        label: '玩家流失'
                    }]
                }, {
                    label: '在线分析'
                }, {
                    label: '大R用户'
                }, {
                    label: '等级分析',
                    children: [{
                        label: '等级详解'
                    }, {
                        label: '等级分布'
                    }, {
                        label: '新玩家进度'
                    }]
                }, {
                    label: '虚拟消费',
                    children: [{
                        label: '虚拟币'
                    }, {
                        label: '消费点'
                    }]
                }, {
                    label: '收入分析',
                    children: [{
                        label: '收入数据'
                    }, {
                        label: '新玩家价值'
                    }, {
                        label: '付费习惯'
                    }, {
                        label: '付费渗透'
                    }]
                }],
                pickerOptions2: {
                    shortcuts: [{
                        text: '最近一周',
                        onClick(picker) {
                            const end = new Date();
                            const start = new Date();
                            start.setTime(start.getTime() - 3600 * 1000 * 24 * 7);
                            picker.$emit('pick', [start, end]);
                        }
                    }, {
                        text: '最近一个月',
                        onClick(picker) {
                            const end = new Date();
                            const start = new Date();
                            start.setTime(start.getTime() - 3600 * 1000 * 24 * 30);
                            picker.$emit('pick', [start, end]);
                        }
                    }, {
                        text: '最近三个月',
                        onClick(picker) {
                            const end = new Date();
                            const start = new Date();
                            start.setTime(start.getTime() - 3600 * 1000 * 24 * 90);
                            picker.$emit('pick', [start, end]);
                        }
                    }]
                },
                //时间值
                value4: '',
                timeValue: '时间未选择',
                gameName: "所有游戏",
                //tag标签数据
                tags: []
            }
        },
        methods: {
            callfilter() {
                Event.$emit('callfilter')
            },
            handleNodeClick(data) {
                console.log(data);
            },
            handleOpen() {
                console.log(this)
            },
            handleClose() {
                console.log(this)
            },
            tagClose(tag) {
                this.tags.splice(this.tags.indexOf(tag), 1);

            },
            rush() {
                this.$confirm("确定退出登录吗,并跳转到登录前页面?", "提示", {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).then(() => {
                    setTimeout(function() {
                        location.href = location.href.split("#")[0]
                    }, 1000)
                    this.$message({
                        type: "success",
                        message: "即将退出",
                    });
                }).catch(() => {
                    this.$message({
                        type: 'info',
                        message: "已取消操作"
                    })
                })
            },
            handleNodeClick(data) {
                switch (data.label) {
                    case '新增玩家':
                        router.push("/home/NewPlayer");
                        break;
                    case '活跃玩家':
                        router.push("/home/JumpPlayer");
                        break;
                    case '玩家留存':
                        router.push("/home/AlivePlayer");
                        break;
                    case '付费转化':
                        router.push("/home/PayPoint");
                        break;
                    case '玩家流失':
                        router.push("/home/RemovePlayer");
                        break;
                    case '设备相关':
                        router.push("/home/UserDevice");
                        break;
                    case '在线分析':
                        router.push("/home/OnlineExp");
                        break;
                    case '大R用户':
                        router.push("/home/RmbPlayer");
                        break;
                    case '等级详解':
                        router.push("/home/LevelInfo");
                        break;
                    case '新玩家进度':
                        router.push("/home/NewPlayerLevel");
                        break;
                    case '等级分布':
                        router.push("/home/LevelPlace");
                        break;
                    case '虚拟币':
                        router.push("/home/VituralMoney");
                        break;
                    case '消费点':
                        router.push("/home/VituralPoint");
                        break;
                    case '收入数据':
                        router.push("/home/GetMoneyData");
                        break;
                    case '新玩家价值':
                        router.push("/home/PlayerToMoney");
                        break;
                    case '付费习惯':
                        router.push("/home/PayWay");
                        break;
                    case '付费渗透':
                        router.push("/home/PayData");
                        break;

                }
            }

        }
    }
</script>
<style lang=sass scoped>
    @import "../sass/home.scss";
</style>