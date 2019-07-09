<template>
	<view>
		<view class="an-week-switch">
			<view class="an-week">
				<view :class="index == weekCur?'an-week-item an-week-item-active':'an-week-item'" v-for="(item, index) in week" :key="index" :style="'width:'+weekItemWH+'px; height:'+weekItemWH+'px; background-size: '+weekItemWH+'px '+weekItemWH+'px;' " @click="onClick(index, weekDay[index].fullDate)">
					<view class="an-week-num" :style="'margin-top:'+(weekItemWH-45)+'px;margin-left:'+(weekItemWH-45)+'px;'">星期{{weekDay[index].week}}</view>
					<view class="an-week-day" :style="'margin-top:2px;margin-left:'+(weekItemWH-45)+'px;'">{{weekDay[index].day}}</view>
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
			}
		},
		data() {
			return {
				weekItemWH: (uni.getSystemInfoSync().windowWidth-8)/7,
				week: ['天', '一', '二', '三', '四', '五', '六'],
				weekDay: [],
				weekCur: this.current,
			};
		},
		watch: {
			current(val) {
				if (val !== this.weekCur) {
					this.weekCur = val;
				}
			}
		},
		mounted() {
			this.loadWeekData();
		},
		methods:{
			onClick(index, fullDate) {
				if (this.weekCur !== index) {
					this.weekCur = index;
					this.$emit('clickItem', index, fullDate);
				}
			},
			loadWeekData(){
				for (var i = 0; i < 7; i++) {
					this.weekDay.push(this.getDayWeek(i));
					console.log(this.getDayWeek(i))
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
				let obj = {
					day: (m<10?'0'+m:m)+'-'+(d<10?'0'+d:d),
					week: this.week[today.getDay()],
					fullDate: y+'-'+(m<10?'0'+m:m)+'-'+(d<10?'0'+d:d)
				};
				return obj;
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
	.an-week-last{
		border-right: 1px solid #CCCCCC;
	}
	.an-week-item-active{
		background-image: url(bg_date.png);
		color: #1d7ffe;
	}
</style>
