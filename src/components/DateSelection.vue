<template>
    <div class="dateBox">
        <div class="dateBoxTit">
            
           <div class="YearMonth">{{showYears}}-{{showMonth}}</div> 

           <div class="perviousMonth MonthSelect" @click="preMonth"><</div>
           <div class="nextMonth MonthSelect" @click="nextMonth">></div>
        </div>
        <div class="week">
            <ul>
                <li>日</li>
                <li>一</li>
                <li>二</li>
                <li>三</li>
                <li>四</li>
                <li>五</li>
                <li>六</li>
            </ul>
        </div>
        <div class="day">
            <ul>
                <li v-for="(item,index) in showDayList" v-bind:class="{now:nowDay== item.daymsg &&showYears == nowYears && showMonth==nowMonth }" @click="checkedDay(item)">{{item.daymsg}}</li>
            </ul>
        </div>
    </div>
</template>
<script>
    export default{
        name:"DateSelection",
        data(){
            return{
                nowYears:2018,//当前年份
                nowMonth:7, //当前显示月份

                showYears:0, //显示的年份
                showMonth:0, //显示月份
                nowDay:12,//当前天数
                nowMonthDay:0,//当前月份的天数
                allDay : [31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31], //每个月的天数
                showDayList:[],
            }
        },
        props:["years","month","day"],
        mounted(){
            // this.nowYears=this.years;
            // this.nowMonth=this.month;
            // this.nowDay=this.day;
            // console.log(this.years+this.month+this.day)
            this.showYears=this.nowYears;
            this.showMonth=this.nowMonth;
            this.showMonthDays();
        },
        watch:{
            years(cur,old){
                if(cur){
                    this.nowYears=cur;
                }
            },
            month(cur,old){
                if(cur){
                    this.nowMonth=cur;
                }
            },
            day(cur,old){
                if(cur){
                    this.nowDay=cur;
                }
            },
        },
        methods:{
            preMonth(){
                if(this.showMonth >1){
                    this.showMonth--;
                    this.showMonthDays();
                }else{
                    this.showMonth=12;
                    this.showYears --;
                    this.showMonthDays();
                }               
            },
            nextMonth(){
                if(this.showMonth >= 12){
                    this.showYears ++;
                    this.showMonth=1;
                    this.showMonthDays();
                }else{
                    this.showMonth++;
                    this.showMonthDays();
                }
                
                
            },
            showMonthDays(){
                this.showDayList=[];
                var date=new Date(this.showYears+"-"+this.showMonth)
                console.log(date);
                date.setDate(1); //时间调整到本月第一天
                var firstDay=date.getDay()//读取本月第一天是星期几
                if(this.showMonth == 2) {
                    if(this.showYears % 4 == 0 && this.showYears % 100 != 0 || this.showYears % 400 == 0) {
                        this.nowMonthDay= 29;
                    }
                }else{
                    this.nowMonthDay= this.allDay[this.showMonth-1];
                    // console.log(this.nowMonthDay)
                }                             
                var j=1; 
                for(let i=0;i<42;i++){
                    let obj={};
                    if(i<firstDay){
                        obj.daymsg="";
                        // obj.pre=true;
                    }else{ 
                        if(j<=this.nowMonthDay){                                                     
                            obj.daymsg=j;
                            //时间前后颜色改变
                            // if(this.showYears < this.nowYears){
                            //     obj.pre=true;
                            // }else if(this.showMonth <this.nowMonth){
                            //     obj.pre=true;
                            // }else{
                            //     obj.pre=false;
                            // }
                            j++;
                        }else{
                            obj.daymsg="";
                            // obj.pre=true;
                        }                   
                    }
                    this.showDayList.push(obj);
                }
            },
            checkedDay(item){
                var curMonth="";
                var curDay="";
                if(this.showMonth<10){
                    curMonth="0"+this.showMonth;
                }else{
                    curMonth=this.showMonth;
                }
                if(item.daymsg<10){
                    curDay="0"+item.daymsg
                } else{
                    curDay=item.daymsg
                }
                var timeMsg=this.showYears+"-"+curMonth+"-"+curDay;
                this.$emit("checekTime",timeMsg)
            }
        }
    }
</script>
<style>
 .dateBox{
     position: absolute;
     width:280px;
     height:250px;
     border:1px solid black;
 }
 .dateBox .dateBoxTit{
     position: relative;
     width:100%;
     height:30px;
     /* border:1px solid black; */
     margin-top:0px;
     line-height: 30px;
     text-align: center;
 }
.dateBox .dateBoxTit .YearMonth{
    width:100%;
    height:30px;
    /* border:1px solid red; */
    border-bottom: 1px solid black;
    
}
.dateBox .dateBoxTit .MonthSelect{
    position: absolute;
    top:0;
    width: 30px;
    height:30px;
    /* border:1px solid grey; */
    cursor: pointer;
}
.nextMonth{
    right:0;
}
.week ul li,.day ul li{
    float: left;
    list-style: none;
    /* border:1px solid black; */
    width:40px;
    height:30px;
    line-height: 30px;
    text-align: center;
    font-size:14px;
    cursor: pointer;
}
.day ul li.pre{
    color:#ccc;
}
.day ul li.now{
    background: red;
    color:#fff;
}
</style>

