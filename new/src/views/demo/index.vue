<template>
	<div class="common-layout">
		<el-container>
			<el-aside width="400px">
				<el-card id="card-left">
					<div id="card-left-box1">
						<span>
							素材生成(未完善)
						</span>
					</div>
					<div id="card-left-box2">
						<span id="card-left-box2-span">素材描述</span>
						<el-card style="width: 360px;height: 220px;" shadow="hover">
							<el-input v-model="text"
								style="width: 360px;height: 220px;position: relative;left: -20px;top: -20px;"
								maxlength="50" placeholder="您可以输入:菠萝,写实风格风车等" show-word-limit type="text" clearable
								class=" demo_input" />
						</el-card>
					</div>
					<div id="card-left-box3">
						<el-button type="primary" @click="onSubmit" id="card-left-box3-el-button">一键生成</el-button>
					</div>
				</el-card>
			</el-aside>
			<el-main>
				<el-card id="card-right">
				<el-card id="card-right-box" shadow='hover'>
					<img src='../../assets/can.png' id="demo_img2"/>
				</el-card>
				<el-card id="card-right-box" shadow='hover'>
					<img src='../../assets/can.png' id="demo_img2"/>
				</el-card>
				</el-card>
			</el-main>
		</el-container>
	</div>
</template>

<script lang="ts" setup>
import { ref } from 'vue';
import { useDemo_imgs } from '../../store';
import { storeToRefs } from 'pinia';
	const useDemo = useDemo_imgs()
	let {demo_list} = storeToRefs(useDemo)
	let {GetDemoImg} = useDemo
	let text =ref()
	const onSubmit = ()=>{
		let data = text.value
		if (data === undefined){
			alert("内容不能为空")
		}
		else{
			GetDemoImg({data})
		}		
		
	}
</script>

<style scoped>
	.common-layout{
		position: relative;
		left: 10px;	
		top:20px;
	}
	.el-aside{
		box-shadow: 5px 10px 5px #d7d4d1;
	}
	#card-left{
		display: flex;
		position: relative;
		height: 490px;
		border-radius: 18px;
	}
	#card-left-box1{
		position: relative;
		left: 115px;
	}
	#card-left-box2{
		position: relative;
		top: 40px;
	}
	#card-left-box2-span{
		display: flex;
		margin-bottom: 15px;
	}
	#card-left-box3-el-button{
		position: relative;
		top:100px;
		width: 350px;
		height: 40px;
		left:6px;
	}
	#card-right{
		display: flex;
		min-width: 180px;
		max-width: 2000px;
	}
	#card-right-box{
		display: flex;
		display: inline-block;
		margin-right: 15px;
		margin-bottom: 10px;
	}
	#demo_img2{
		width: 100px;
		height: 100px;
	}
</style>