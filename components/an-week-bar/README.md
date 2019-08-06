### AnWeekBar 日期周条使用说明

> 引入组件：

```
import anWeekBar from "@/components/an-week-bar/an-week-bar.vue"

export default {
	components:{
		anWeekBar
	},
}
```

> 使用组件

```
<an-week-bar :current="weekCur" @clickItem="weekItemClick"></an-week-bar>

data() {
	return {
		weekCur: 0,
	}
},

method: {
	//日期切换时  index 当前选中的索引，fullDate 当前选中的日期(格式为 yyyy-mm-dd)
	weekItemClick(index, fullDate){
		this.weekCur = index;
		this.curDate = fullDate;
		// TODO 当选中后刷新你的数据
	},
}

```

> 属性

属性名 | 类型 | 默认值 | 说明 | 平台差异说明 
-|-|-
current | Number | 0 | 默认选中，从0开始 | 无 
@clickItem | String | "#7C7C7C" | 虚线框颜色 | 无

> 事件

事件名 | 类型 | 参数 | 平台差异说明 
-|-|-
@clickItem | click | index 当前选中的坐标, fullDate 当前选中的日期，是全的格式为：yyyy-mm-dd | 无