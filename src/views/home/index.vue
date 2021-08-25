<template>
    <div class="index">
        <el-row :gutter="20" >
            <el-col :span="6" v-for="(item,index) in counts" :key ="index">
                <el-card class="box-card" shadow="hover" >
                    <div class="d-flex align-items-center">
                        <i class="h4 mb-0 bg-primary text-white text-center mr-3 icon-user"
                            :class="[item.icon,item.color]"></i>
                        <div>
                            <h4 class="mb-0">{{item.num}}</h4>
                            <small class="text-muted">{{item.desc}}</small>
                        </div>
                    </div>
                </el-card>

            </el-col>
        </el-row>


        <el-row :gutter='20' class="mt-3">
            <el-col :span="12" style="height: 370px" class="d-flex flex-column">
                <el-card shadow="hover" class="box-card mb-auto" v-for="(item,index) in tips" :key="index">
                    <div slot="header" class="clearfix">
                       <span>{{item.title}}</span>
                        <el-button style="float: right; padding: 3px 0" type='text'>{{item.desc}}</el-button>
                    </div>
                    <div class="row">
                        <div :class="item.list.length | getCol" v-for="(list,index) in item.list" :key="index">
                            <button class="btn btn-light w-100">
                                <h4 class="mb-1">{{list.value}}</h4>
                                <small class="text-muted">{{list.name}}</small>
                            </button>
                        </div>
                    </div>
                </el-card>
            </el-col>
            <el-col :span="12">
                <el-card shadow="hover" class="box-card" style="height: 370px">
                    <div slot="header" class="clearfix">
                       <span>店铺名称</span>
                        <el-button style="float: right; padding: 3px 0" type='text'>操作按钮</el-button>
                    </div>
                    <div ref="myChart" style="width: 100%; height: 270px"></div>
                </el-card>
            </el-col>
        </el-row>

        <el-row :gutter ='20' class="mt-3">
            <el-col :span ="12">
                <el-card shadow="hover" class="box-card">
                    <div slot="header" class="clearfix">
                       <span>店铺名称</span>
                        <el-button style="float: right; padding: 3px 0" type='text'>操作按钮</el-button>
                    </div>
                    <div class="media align-items-center border">
                        <span class="py-4 px-3 bg-light border-right">昨日销量</span>
                        <div class="media-body">
                            <div class="pl-3 pb-2 mb-1 order"><span>订单量(件)</span>12</div>
                            <div class="pl-3"><span>订单金额(元)</span>12</div>
                        </div>
                    </div> 
                    <div class="media align-items-center border mt-3">
                        <span class="py-4 px-3 bg-light border-right">本月销量</span>
                        <div class="media-body">
                            <div class="pl-3 pb-2 mb-1 order"><span>订单量(件)</span>12</div>
                            <div class="pl-3"><span>订单金额(元)</span>12</div>
                        </div>
                    </div>
                </el-card>
            </el-col>
             <el-col :span="12">
                <el-card shadow="hover" class="box-card" style="height: 300px">
                    <div slot="header" class="clearfix">
                       <span>单品销售排名</span>
                        <el-button style="float: right; padding: 3px 0" type='text'>按周期统计商家店铺的订单量和订单金额</el-button>
                    </div>

                    <el-table
                        :data="tableData"
                        height="180"
                        border
                        style="width: 100%">
                        <el-table-column
                        type="index"
                        label="#"
                        width="50">
                        </el-table-column>
                        <el-table-column
                        prop="name"
                        label="商品信息"
                            >
                        </el-table-column>
                        <el-table-column
                        prop="num"
                        label="销量"
                        width="50">
                        </el-table-column>
                    </el-table>
                </el-card>
            </el-col>
        </el-row>
    </div>
</template>

<script >
import * as echarts from 'echarts';
export default {
    name: "",
    data() {
        return {
            tableData:[


                {name:"小天鹅（LittleSwan）滚筒洗衣机...",num: 9},
                {name:"小天鹅（LittleSwan）滚筒洗衣机...",num: 9},
                {name:"小天鹅（LittleSwan）滚筒洗衣机...",num: 9},
                {name:"小天鹅（LittleSwan）滚筒洗衣机...",num: 9},
                {name:"小天鹅（LittleSwan）滚筒洗衣机...",num: 9},
                {name:"小天鹅（LittleSwan）滚筒洗衣机...",num: 9}

            ],
            counts:[
                {
                    icon: "el-icon-user-solid",
                    num: "30",
                    color:'bg-primary',
                    desc:"关注人数(个数)"
                },
                {
                    icon: "el-icon-s-finance",
                    num: "120",
                    color:'bg-success',
                    desc:"订单总数"
                },
                {
                    icon: "el-icon-s-order",
                    num: "4183.80",
                    color:'bg-danger',
                    desc:"今日订单总金额"
                },
                {
                    icon: "el-icon-s-data",
                    num: "100",
                    color:'bg-warning',
                    desc:"本月销量(笔)"
                }
            ],
            tips:[

                {
                    title: "店铺及商品提示",
                    desc:"需要关注店铺信息及待处理事项",
                    list:[
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"}
                    ]
                },
                {
                   title: "店铺及商品提示",
                    desc:"需要关注店铺信息及待处理事项",
                    list:[
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"},
                        {name:"出售中",value: "64"}
                    ]
                }
            ],
            
        }
    },
    components: {},
    methods: {

        drawLine() {
        let myChart =  echarts.init(this.$refs.myChart);
        var option =option = {
                        tooltip: {
                            trigger: 'axis',
                            axisPointer: {
                                type: 'cross',
                                label: {
                                    backgroundColor: '#6a7985'
                                }
                            }
                        },
                        legend: {
                            data: ['邮件营销', '联盟广告', '视频广告', '直接访问', '搜索引擎']
                        },
                        toolbox: {
                            feature: {
                                saveAsImage: {}
                            }
                        },
                        grid: {
                            left: '3%',
                            right: '4%',
                            bottom: '3%',
                            containLabel: true
                        },
                        xAxis: [
                            {
                                type: 'category',
                                boundaryGap: false,
                                data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
                            }
                        ],
                        yAxis: [
                            {
                                type: 'value'
                            }
                        ],
                        series: [
                            {
                                name: '邮件营销',
                                type: 'line',
                                stack: '总量',
                                areaStyle: {},
                                emphasis: {
                                    focus: 'series'
                                },
                                data: [120, 132, 101, 134, 90, 230, 210]
                            },
                            {
                                name: '联盟广告',
                                type: 'line',
                                stack: '总量',
                                areaStyle: {},
                                emphasis: {
                                    focus: 'series'
                                },
                                data: [220, 182, 191, 234, 290, 330, 310]
                            },
                            {
                                name: '视频广告',
                                type: 'line',
                                stack: '总量',
                                areaStyle: {},
                                emphasis: {
                                    focus: 'series'
                                },
                                data: [150, 232, 201, 154, 190, 330, 410]
                            },
                            {
                                name: '直接访问',
                                type: 'line',
                                stack: '总量',
                                areaStyle: {},
                                emphasis: {
                                    focus: 'series'
                                },
                                data: [320, 332, 301, 334, 390, 330, 320]
                            },
                            {
                                name: '搜索引擎',
                                type: 'line',
                                stack: '总量',
                                label: {
                                    show: true,
                                    position: 'top'
                                },
                                areaStyle: {},
                                emphasis: {
                                    focus: 'series'
                                },
                                data: [820, 932, 901, 934, 1290, 1330, 1320]
                            }
                        ]
        };
        
        myChart.setOption(option)

        }
    },
    filters:{
        getCol(value) {
            var col =12 / value;
            return `col-${col}` ;
        }
    },
    mounted() {
        this.drawLine();
    }
}
</script>

<style scoped>
    .icon-user {
       width:40px ;
       height: 40px;
       line-height: 40px;
    }
    .order {
        border-bottom: 1px solid #f1f1f1;
    }
    .index  {
        padding: 20px;
    }
</style>
