<template>
	<div class="common-layout">
		<el-container>
			<el-header>
				<div>
					<span id="more-font">包装探索(未完善)</span>
				</div>
				<div id="more-box">
					<input v-model="content" :placeholder="place" id="more-search"   @keyup.enter.native="search"/>
					<button id="more-botton" @click="search"><span id="more-botton-span">搜索</span></button>
				</div>
			</el-header>
			<el-main>
				<div id="main-box">
					<el-space wrap>
						<el-card v-for="item in 20"  id="img-card" shadow="hover">
							<a href="#">
							<img src="../../assets/can.png" id="img2" v-bind:title="666"/>
							</a>
						</el-card>
					</el-space>
				</div>
			</el-main>
		</el-container>
	</div>
</template>

<script lang="ts" setup>
import { storeToRefs } from 'pinia';
import { useMore_imgs } from '../../store';
import { ref } from 'vue';
	let content = ref('')
	let place = ref('')
	const usemore = useMore_imgs()
	const {more_list,Content} = storeToRefs(usemore)
	const { GetMore,Search } = usemore
	if (Content.value === ''){
		place.value ='请输入关键字'
	}
	else{
	content.value=Content.value
	}
	GetMore()
	const search = () =>{
		if(content.value ===''){
			GetMore()			
		}
		else{
			let data = content.value
			Search({data})			
		}
	}
</script>

<style scoped>
	.common-layout{
		width: 1750px;
		min-height: 2000px;
		height: 100vh;
		background: linear-gradient(to bottom, #EAD6EE 0%, #f4d7b1 50%);
		position: relative;
		left: 10px;
		top: 20px;
	}
	#more-box {
		position: relative;
		left: 570px;
		top: 160px;
		max-width: 600px;
	}

	#more-search {
		display: flex;
		width: 470px;
		height: 50px;
		border-radius: 30px;
	}

	#more-botton {
		display: flex;
		position: relative;
		left: 385px;
		top: -48px;
		width: 80px;
		height: 40px;
		border-radius: 20px;
	}
	#more-botton-span{
		display: flex;
		position: relative;
		left: 17px;
		top: 6px;
		font-size: 15px;
	}
	#more-font {
		position:relative;
		left: 700px;
		top: 120px;
		font-size: 30px;
		color: #eb700d;
	}
	.el-main{
		min-width: 1400px;
	}
	#main-box{
		display: flex;
		margin-top: 250px;
		max-width: 1680px;
	}
	#img-card {
		position: relative;
		left: 60px;
		width: 240px;
		height: 240px;
	}
	#img2{
		position: relative;
		left: -20px;
		top: -20px;
		width: 240px;
		height: 240px;
	}
</style>