<template>
  <div class="main">
     <p v-bind:class="{ active: isActive, 'text-danger': hasError}">我是一条小青龙</p>
     <button @click="trun">切换</button>
     <comment hidden/>
     <p>二</p>
     <child @getchild='yeschild'></child>
     <p >{{message}}</p>
     <el-select v-model="value" placeholder="请选择">
        <el-option
        v-for="item in options"
        :key="item.value"
        :label="item.label+item.tt==null?'':item.tt"
        :value="item.value">
        </el-option>
    </el-select>
    <div v-for="(item,index) in list" :ref="setItemRef" :key="index" @click="op">{{item}}</div>
  </div>
</template>

<script>
import Child from './child.vue';
import Comment from './Comment.vue';

export default {
    
  components: { Comment,Child },
    
    Childname:'Main',
    data(){
        return{
            isActive: true,
            hasError: false,
            message:'',
            options: [{
                value: '选项1',
                label: '黄金糕',
                tt: '公司'
                }, {
                value: '选项2',
                label: '双皮奶',
                tt :null
                }, {
                value: '选项3',
                label: '蚵仔煎',
                tt :null
                }, {
                value: '选项4',
                label: '龙须面',
                tt :null
                }, {
                value: '选项5',
                label: '北京烤鸭',
                tt :null
                }],
            value: '',
            itemRefs: [],
            list:[1,2,3,4,5,6,7]
        }
    },
    methods:{
        trun(){
            this.isActive=!this.isActive;
            this.hasError=!this.hasError;
            
        },
        yeschild(value){
            this.message='请稍后...'
            setTimeout(() => {
                this.message=value
            }, 2000);
        },
        setItemRef(el) {
        if (el) {
            this.itemRefs.push(el)
            }
        },
        op(){
            console.log(this)
        }
    },
    beforeUpdate() {
        this.itemRefs = []
    },
    updated() {
        console.log(this.itemRefs)
    }
}
</script>

<style scoped>
.active{
    color: red;
}
.text-danger{
    color: blue;
}

</style>