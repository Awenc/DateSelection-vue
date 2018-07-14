
## 这是一个简单的Vue日期选择器

### 点击选择日期  可以弹出一个简单的日期选择器

### 点击某一天的日期  这个日期将会显示在文本框中

## DateSelection.vue为日期组件

### 利用date函数 和相应的方法实现每个月的天数展示
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
                    j++;
                }else{
                    obj.daymsg="";
                    // obj.pre=true;
                }                   
            }
            this.showDayList.push(obj);
        }
    },

### 然后利用父子组件之间的传值 

### ps 本人菜鸟 虽然实现了这个效果  但是这个组件实在是太丑了而且自己感觉方法有点傻逼  后期需要大量的改进
