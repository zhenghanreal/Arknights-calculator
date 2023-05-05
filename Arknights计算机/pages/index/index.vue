<template>
	<view class="index">
		<view class="tag">
			<view class="top">
				<text class="title">Tag列表</text>
				<button class="tip" @click="open">提示</button>
				<uni-popup ref="popup" type="center" background-color="#222a35">
					<view class="tip_box">
						<text>招募小提示\n
						1.出现“<text class="red">资深干员</text>”或“<text class="red">高级资深干员</text>”时间拉满9小时必定出5星和6星\n
						2.出现“<text class="red">支援机械</text>”出一星机器人要把时间调整为3小时50分\n
						3.部分tag必出4星及以上的干员刷出了请留意\n
						<text class="red">特种</text>，<text class="red">削弱</text>，<text class="red">位移</text>，<text class="red">爆发</text>，<text class="red">控场</text>，<text class="red">召唤</text>，<text class="red">支援</text>，<text class="red">快速复活</text></text>
					</view>
				</uni-popup>
			</view>
			<view class="divider"></view>
			<view class="occupation"><!-- 职位 -->
				<ul>
					<li v-for="item in occupation" :key="item.id">
						<button @click="checks(item)" ref="btn" :class="item.className">{{item.name}}</button>
					</li>
				</ul>
			</view>
			<view class="type"><!-- 功能 -->
				<ul>
					<li v-for="item in type" :key="item.id">
						<button @click="checks(item)" ref="btn" :class="item.className">{{item.name}}</button>
					</li>
				</ul>
			</view>
			<view class="ability"><!-- 类型 -->
				<ul>
					<li v-for="item in ability" :key="item.id">
						<button @click="checks(item)" ref="btn" :class="item.className">{{item.name}}</button>
					</li>
				</ul>
			</view>
			<view class="divider"></view>
			<view class="reset">
				<button @click="resetbtn()" class="reset_btn">重置</button>
			</view>
		</view>
		<result :values="values"></result>
	</view>
</template>

<script>
	import Result from '../Result/index.vue'
	export default {
		data() {
			return {
				occupation:[
					{check:true,className:"btn",name:'先锋',id:0},
					{check:true,className:"btn",name:'近卫',id:1},
					{check:true,className:"btn",name:'重装',id:2},
					{check:true,className:"btn",name:'狙击',id:3},
					{check:true,className:"btn",name:'术士',id:4},
					{check:true,className:"btn",name:'医疗',id:5},
					{check:true,className:"btn",name:'辅助',id:6},
					{check:true,className:"btn",name:'特种',id:7},
				],
				type:[
					{check:true,className:"btn",name:'新手',id:8},
					{check:true,className:"btn",name:'资深干员',id:9},
					{check:true,className:"btn",name:'高级资深干员',id:10},
					{check:true,className:"btn",name:'远程位',id:11},
					{check:true,className:"btn",name:'近战位',id:12},
				],
				ability:[
					{check:true,className:"btn",name:'治疗',id:13},
					{check:true,className:"btn",name:'支援',id:14},
					{check:true,className:"btn",name:'输出',id:15},
					{check:true,className:"btn",name:'群攻',id:16},
					{check:true,className:"btn",name:'减速',id:17},
					{check:true,className:"btn",name:'生存',id:18},
					{check:true,className:"btn",name:'防护',id:19},
					{check:true,className:"btn",name:'削弱',id:20},	
					{check:true,className:"btn",name:'位移',id:21},	
					{check:true,className:"btn",name:'爆发',id:22},	
					{check:true,className:"btn",name:'控场',id:23},	
					{check:true,className:"btn",name:'召唤',id:24},	
					{check:true,className:"btn",name:'快速复活',id:25},	
					{check:true,className:"btn",name:'费用回复',id:26},	
					{check:true,className:"btn",name:'支援机械',id:27},	
				],
				num:0,
				values:[],
				flag:true
				}
		},
		components:{
			Result
		},
		methods:{
			resetbtn(){
				this.values = []
				this.num = 0
				for(let i=0; i<this.occupation.length; i++){
					this.occupation[i].className = 'btn'
					this.occupation[i].check = 'true'
				}
				for(let i=0; i<this.type.length; i++){
					this.type[i].className = 'btn'
					this.type[i].check = 'true'
				}
				for(let i=0; i<this.ability.length; i++){
					this.ability[i].className = 'btn'
					this.ability[i].check = 'true'
				}
			},
			checks(item){
				if(item.check){
					if(this.num>=6){
						alert("最多只能同时选择 6 个词条哦")
						return
					}
					item.className = 'pickbtn'
					item.check = false
					this.num++
					this.values.push(item.name)
				}else{
					item.className = 'btn'
					item.check = true
					this.num--
					this.values = this.values.filter(value=>{
						let check = true
						if(value === item.name){
							check = false
						}
						return check
					})
				}
			},
			open(){
			    this.$refs.popup.open()
			}
		}
	}
</script>

<style lang="scss" scoped>
	.index{
		width: 100%;
		height: 100vh;
		background-color: #222a35;
		
		.tag{
			height: auto;
			position: relative;
			
			.divider{
				background: #E0E3DA;
				width: 100%;
				height: 5rpx;
				margin: 10rpx 0;
			}
			
			.top{
				padding: 10rpx 0;
				position: relative;
				
				.title{
					padding-top: 10rpx;
					font-size: 35rpx;
					margin-left: 30rpx;
					height: 70rpx;
					line-height: 60rpx;
					color: white;
				}
				
				.tip{
					position: absolute;
					top:20rpx;
					right: 30rpx;
					color: black;
					background-color: #eeeeee;
					font-size: 26rpx;
					width: auto;
					height: 50rpx;
					line-height: 50rpx;
				}
				
				.tip_box{
					font-size: 30rpx;
					width: 700rpx;
					margin: auto;
					padding: 15rpx;
					line-height: 50rpx;
					color: #eeeeee;
					
					.red{
						color: #ec0003;
					}
				}
			}
			
			.occupation,
			.ability,
			.type{
				ul{
					padding: 5rpx 20rpx;
					display: flex;
					flex-wrap: wrap;
					
					li{
						margin: 10rpx;
						.btn{
							color: black;
							background-color: #eeeeee;
							font-size: 26rpx;
							width: auto;
							height: 50rpx;
							line-height: 50rpx;
						}	
						.pickbtn{
							color: white;
							background-color: #0295de;
							font-size: 26rpx;
							width: auto;
							height: 50rpx;
							line-height: 50rpx;
						}	
					}
				}
			}
			
			.reset{
				box-sizing: border-box;
				position: relative;
				width: 100%;
				height: 75rpx;
				padding: 15rpx;
				
				.reset_btn{
					position: absolute;
					left: 30rpx;
					font-size: 30rpx;
					width: 130rpx;
					height: 60rpx;
					line-height: 60rpx;
					background-color: orangered;
					color: white;
				}
			}
		}
		
	}
</style>
