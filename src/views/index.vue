<template>
    <div>
        <div>日期选择器</div>
        <div>
            <input type="text" v-model="time">
            <div class="SelectBtn" @click="selectDate">点击选择日期</div>
            <date-selection v-on:checekTime="showTime" v-show="isShowTime" :years="nowYears" :month="nowMonth" :day="nowDay"></date-selection>
        </div>
    </div>
</template>
<script>
    import DateSelection from "@/components/DateSelection"
    export default{
        name:"index",
        data(){
            return{
                time:"",
                isShowTime:false,
                showX:0,
                showY:0,
                nowYears:'',
                nowMonth:'',
                nowDay:'',
            }
        },
        components:{
            DateSelection
        },
        
        methods:{
            showTime(e){
                this.time=e;
                this.isShowTime=false;
            },
            selectDate(e){
                this.isShowTime=true;
                // console.log(e);
                var date=new Date();
                this.nowYears=date.getFullYear();
                this.nowMonth=date.getMonth()+1;
                this.nowDay=date.getDate();
                // console.log(this.nowYears+"..."+this.nowMonth+"..."+this.nowDay);
            }
        }
    }
</script>
<style>
    .SelectBtn{
        margin-top:10px;
        width:100px;
        height:30px;
        text-align: center;
        line-height: 30px;
        background: grey;
        color:#fff;
        font-size:14px;
        cursor: pointer;
    }

</style>
