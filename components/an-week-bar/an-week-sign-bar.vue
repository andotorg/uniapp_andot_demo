<template>
	<view>
		<view class="an-week-switch">
			<view class="an-week" :style="'height: '+weekItemWH+'px;'">
				<view class="an-week-item" :style="'width:'+weekItemWH+'px; height:'+weekItemWH+'px; line-height:'+weekItemWH+'px; text-align: center;'">
					<view class="an-week-num">时间</view>
				</view>
				<view class="an-week-item" v-for="(item, index) in week" :key="index" :style="'width:'+weekItemWH+'px; height:'+weekItemWH+'px; background-size: '+weekItemWH+'px '+weekItemWH+'px;'">
					<view class="an-week-num" :style="'margin-top:'+(weekItemWH-40)+'px;margin-left:'+(weekItemWH-40)+'px;'">星期{{weekDay[index].week}}</view>
					<view class="an-week-day" :style="'margin-top:2px;margin-left:'+(weekItemWH-40)+'px;'">{{weekDay[index].day}}</view>
				</view>
				<view :style="'width: 1px; height: '+(weekItemWH+2)+'px; background-color:#CCCCCC; float: left;'"></view>
			</view>
			<view class="an-week" :style="'height: '+(weekItemWH+4)+'px;'" v-for="(value, key) in dayTime" :key="key">
				<view class="an-week-item clear-border" :style="'width:'+weekItemWH+'px; height:'+weekItemWH+'px; line-height:'+weekItemWH+'px; text-align: center;margin-top:-'+(key=='am'?1:2)+'px;'">
					<view class="an-week-num">{{value}}</view>
				</view>
				<view class="an-week-item" v-for="(item, index) in ndata[key]" :key="index"  @click="onClick(index, item, weekDay[index].fullDate)"
						:style="'width:'+weekItemWH+'px; height:'+weekItemWH+'px; background-size: '+weekItemWH+'px '+weekItemWH+'px; line-height:'+weekItemWH+'px; text-align: center; margin-top:-'+(key=='am'?1:2)+'px; background-color: '+ndata.bgColors[item-1]+'; color:'+ndata.txtColors[item-1]">
					<view class="an-week-num">{{ndata.title[item-1]}}</view>
				</view>
				<view :style="'width: 1px; height: '+(weekItemWH+2)+'px; background-color:#CCCCCC; float: left;'"></view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		props:{
			current: {
				type: Number,
				default: 0
			},
			date: {
				type: String,
				default: '0'
			},
			ndata: {
				type: Object,
				default: ()=>{
					return {
						am: [],
						pm: [],
						title: [],
						bgColors: [],
						txtColors: [],
					};
				}
			},
		},
		data() {
			return {
				dayTime: {
					am: '上午', 
					pm: '下午'
				},
				weekItemWH: (uni.getSystemInfoSync().windowWidth-9)/8,
				week: ['天', '一', '二', '三', '四', '五', '六'],
				weekDay: this.loadWeekData(),
			};
		},
		mounted() {
			if(typeof(this.ndata.am) != 'undefined' && typeof(this.ndata.pm) != 'undefined'){
				if(this.ndata.am.length > 7 || this.ndata.pm.length > 7){
					console.error("[am] and [pm] array length only 7, beyond non-display! ");
					console.error("[am] and [pm] 数组长度只能 7, 超出则不显示！ ");
				}
			}else{
				console.error("[ndata] must include key [am] and [pm] 的数组! ");
				console.error("[ndata] 必须包含键 [am] and [pm] 的数组！");
			}
		},
		methods:{
			onClick(index, value, fullDate) {
				this.$emit('clickItem', index, value, fullDate);
			},
			loadWeekData(){
				if(this.check()){
					return;
				}
				for (var i = 0; i < 7; i++) {
					this.weekDay.push(this.getDayWeek(i));
				}
			},
			getDayWeek(day){
				let today = new Date(this.date);
				if(this.date == '0'){
					today = new Date();
				}
				let targetday_milliseconds = today.getTime() + 1000*60*60*24*day;
				today.setTime(targetday_milliseconds); //注意，这行是关键代码
				let y = today.getFullYear();
				let m = today.getMonth()+1;
				let d = today.getDate();
				let weeks = ['天', '一', '二', '三', '四', '五', '六'];
				let obj = {
					day: (m<10?'0'+m:m)+'-'+(d<10?'0'+d:d),
					week: weeks[today.getDay()],
					fullDate: y+'-'+(m<10?'0'+m:m)+'-'+(d<10?'0'+d:d)
				};
				return obj;
			},
			check(){
				if(typeof(this.ndata.am) != 'undefined' && typeof(this.ndata.pm) != 'undefined'){
					if(this.ndata.am.length > 7 || this.ndata.pm.length > 7){
						console.error("[am] and [pm] array length only 7, beyond non-display! ");
						console.error("[am] and [pm] 数组长度只能 7, 超出则不显示！ ");
						return true;
					}
				}else{
					console.error("[ndata] must include key [am] and [pm] 的数组! ");
					console.error("[ndata] 必须包含键 [am] and [pm] 的数组！");
					return true;
				}
				return false;
			}
		}
	}
</script>

<style>
	.an-week-switch{
		background-color: #FFFFFF;
	}
	.an-week{
		height: 120upx;
	}
	.an-week-item{
		border-top: 1px solid #CCCCCC;
		border-left: 1px solid #CCCCCC;
		border-bottom: 1px solid #CCCCCC;
		font-size: 12px;
		float: left;
	}
	.an-week-item:active{
		background-color: #dfdfdf;
	}
	.an-week-last{
		border-right: 1px solid #CCCCCC;
	}
	
	.clear-border{
		margin-top:-1px
	}
</style>
