<template>
	<view class="result">
		<view class="type_card" v-for="item in result" :key="item.tag"><!-- 信息卡 -->
			<view class="tag">
				<text class="tag_text" v-for="tag in item.checkTag">{{tag}}</text>
			</view>
			<view ref="role" class="role_card" v-for="info in item.data" :key="info.name">
				<view class="role_name">{{info.name}}</view>
				<view class="role_content">
					<view class="role_content_view" :style="{backgroundColor:info.color}">{{info.rank}}</view>
					<view class="role_content_view">{{info.type[1]}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import data1 from '../../static/data/data1.json'
	import data2 from '../../static/data/data2.json'
	export default{
		data(){
			return{
				fiveS:data1,
				SixS:data2,
			}
		},
		props:{
			values:{
				type:Array,
			}
		},
		// created() {
		// 	//发送请求
		// 	uni.request({
		// 	    url:'../../static/data/data1.json', 
		// 	    success: (res) => {
		// 	        this.fiveS = res.data
		// 	    }
		// 	});
		// 	uni.request({
		// 	    url:'../../static/data/data2.json', 
		// 	    success: (res) => {
		// 	        this.SixS = res.data
		// 	    }
		// 	});
		// },
		computed:{
			//过滤数据
			result(){
				//存放全部数据
				const allData = []
				//存放单次循环的数据
				let eachData = []
				//2组合标签合集
				const doubleTag = []
				//3组合标签合集
				const tripleTag = []
				//创建2组合标签
				for(let i = 0; i<this.values.length; i++){
					for(let j = i+1; j<this.values.length; j++){
						doubleTag.push([this.values[i],this.values[j]])
					}
				}
				//创建3组合标签
				for(let i = 0; i<this.values.length; i++){
					for(let j = i+1; j<this.values.length; j++){
						for(let k = j+1; k<this.values.length; k++){
								tripleTag.push([this.values[i],this.values[j],this.values[k]])
						}
					}
				}	
				//录入3组合标签(6星)
				for(let i = 0; i<tripleTag.length; i++){
					eachData = this.SixS.filter(item =>{
						let check = false
						if(tripleTag[i].includes("高级资深干员")){
							if(JSON.parse(JSON.stringify(item)).type.includes(tripleTag[i][0])){
								if(JSON.parse(JSON.stringify(item)).type.includes(tripleTag[i][1])){
									if(JSON.parse(JSON.stringify(item)).type.includes(tripleTag[i][2])){
										check = true
									}
								}
							}
						}				
						return check
					})
					//获取多次循环的数据
					if(eachData!=''){
						allData.push({checkTag:tripleTag[i],data:eachData})
					}
				}
				//录入2组合标签(6星)
				for(let i = 0; i<doubleTag.length; i++){
					eachData = this.SixS.filter(item =>{
						let check = false
						if(doubleTag[i].includes("高级资深干员")){
							if(JSON.parse(JSON.stringify(item)).type.includes(doubleTag[i][0])){
								if(JSON.parse(JSON.stringify(item)).type.includes(doubleTag[i][1])){
									check = true
								}
							}
						}
						return check
					})
					//获取多次循环的数据
					if(eachData!=''){
						allData.push({checkTag:doubleTag[i],data:eachData})
					}
				}
				//录入单标签(6星)
				for(let i = 0; i<this.values.length; i++){
					eachData = this.SixS.filter(item =>{
						let check = false	
						if(this.values[i].includes("高级资深干员")){
							if(JSON.parse(JSON.stringify(item)).type[0].includes(this.values[i])){
								check = true
							}
						}
						return check
					})
					//获取多次循环的数据
					if(eachData!=''){
						allData.push({checkTag:[this.values[i]],data:eachData})
					}
				}
				//录入3组合标签(5星)
				for(let i = 0; i<tripleTag.length; i++){
					eachData = this.fiveS.filter(item =>{
						let check = false
						if(JSON.parse(JSON.stringify(item)).type.includes(tripleTag[i][0])){
							if(JSON.parse(JSON.stringify(item)).type.includes(tripleTag[i][1])){
								if(JSON.parse(JSON.stringify(item)).type.includes(tripleTag[i][2])){
									check = true
								}
							}
						}
						return check
					})
					//获取多次循环的数据
					if(eachData!=''){
						allData.push({checkTag:tripleTag[i],data:eachData})
					}
				}
				//录入2组合标签(5星)
				for(let i = 0; i<doubleTag.length; i++){
					eachData = this.fiveS.filter(item =>{
						let check = false
						if(JSON.parse(JSON.stringify(item)).type.includes(doubleTag[i][0])){
							if(JSON.parse(JSON.stringify(item)).type.includes(doubleTag[i][1])){
								check = true
							}
						}
						return check
					})
					//获取多次循环的数据
					if(eachData!=''){
						allData.push({checkTag:doubleTag[i],data:eachData})
					}
				}
				//录入单标签(5星)	
				for(let i = 0; i<this.values.length; i++){
					eachData = this.fiveS.filter(item =>{
						let check = false	
						if(JSON.parse(JSON.stringify(item)).type.includes(this.values[i])){
							check = true
						}
						return check
					})
					//获取多次循环的数据
					if(eachData!=''){
						allData.push({checkTag:[this.values[i]],data:eachData})
					}
				}
				return allData
			}
		},
	}
</script>

<style lang="scss" scoped>
	.result{
		padding: 10rpx;
		background-color: #222a35;
		height: auto;
		display: flex;
		flex-direction: column;
		overflow: auto;
		
		.type_card{
			width: 100%;
			height: auto;
			line-height: 70rpx;
			background-color: #222a35;
			box-sizing: border-box;
			padding: 0 10rpx;
			display: flex;
			flex-wrap: wrap;
			
			.tag{
				width: 100%;
				
				.tag_text{
					border-radius: 5rpx;
					padding: 8rpx 20rpx;
					margin-left: 10rpx;
					background-color: #0295de;
					color: #eeeeee;
				}
			}
			
			.role_card{
				border-radius: 10rpx;
				font-size: 30rpx;
				margin: 10rpx;
				width: 30%;
				height: 100rpx;
				line-height: 45rpx;
				background-color: #eeeeee;
				box-sizing: border-box;
				padding: 0 10rpx;
				
				.role_name{
					font-weight: bold;
					margin-left: 5rpx;
				}
				
				.role_content{
					display: flex;
					
					.role_content_view{
						width: auto;
						padding: 0rpx 10rpx;
						border-radius: 10rpx;
						margin: 0rpx 5rpx;
					}
				}
			}
		}
	}
</style>