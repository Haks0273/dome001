<template>
	<div class="common-layout">
		<el-container>
			<el-header>
				<div id="header">
					<span id="title1">包装设计进入</span>
					<span id="title2">AI时代</span>
					<div id="head-box">
						<input v-model="content" placeholder="请输入:" id="head-search" @keyup.enter.native="search" />
						<button id="head-botton" @click="search">发送</button>
					</div>
					<rollVue></rollVue>
				</div>
			</el-header>
			<el-main>
				<div id="head-main-box1">
					<div>
						<span id="head-main-box1-span1">AI生图</span><br />
						<span id="head-main-box1-span2">创意无限</span>
					</div>
					<el-space wrap>
						<el-card v-for="(item,index) in img_list" :key="index" id="head-main-box1-card" shadow="hover">
							<router-link to="/createtool">
								<img :src="item" id="img1">
							</router-link>
						</el-card>
					</el-space>
				</div>
				<div id="head-main-box2">
					<div style="width: 130px;">
						<span id="head-main-box2-span1">思维碰撞</span><br />
						<span id="head-main-box2-span2">创意无限</span>
					</div>
					<el-space wrap>
						<el-card v-for="item in 10" id="head-main-box2-card" shadow="hover">
							<router-link to="/more">
								<img src="../../assets/can.png" id="img2">
							</router-link>
						</el-card>
					</el-space>
				</div>
				<div id="head_bottom1">
					<div id="head_bottom2">
						<router-link to="/more">
							<el-button id="head_bottom3">
								<svg t="1730628489089" class="icon" viewBox="0 0 1024 1024" version="1.1"
									xmlns="http://www.w3.org/2000/svg" p-id="4434" width="50" height="50">
									<path
										d="M835.920926 709.185988c38.736233-63.135946 60.438511-149.049664 60.438511-228.548276 0-229.402737-185.964412-415.372266-415.367149-415.372266-229.39762 0-415.368172 185.969529-415.368172 415.372266 0 229.398644 185.969529 415.367149 415.368172 415.367149 74.952063 0 145.265478-19.851117 205.973118-54.586223 31.038924-17.758456 173.628456 155.566078 246.050905 110.546745C1019.28614 898.334929 818.068326 738.276537 835.920926 709.185988zM301.696762 533.598924c-31.378661 0-56.814983-25.438369-56.814983-56.816007s25.436322-56.816007 56.814983-56.816007c31.379685 0 56.814983 25.438369 56.814983 56.816007S333.076446 533.598924 301.696762 533.598924zM479.332485 533.598924c-31.378661 0-56.81703-25.438369-56.81703-56.816007s25.438369-56.816007 56.81703-56.816007 56.814983 25.438369 56.814983 56.816007S510.711146 533.598924 479.332485 533.598924zM656.966161 533.598924c-31.377638 0-56.814983-25.438369-56.814983-56.816007s25.437345-56.816007 56.814983-56.816007c31.378661 0 56.81703 25.438369 56.81703 56.816007S688.344822 533.598924 656.966161 533.598924z"
										fill="#8a8a8a" p-id="4435"
										data-spm-anchor-id="a313x.search_index.0.i0.39963a81PExDVG" class="selected">
									</path>
								</svg>
							</el-button>
						</router-link>
					</div>
				</div>
			</el-main>
		</el-container>
	</div>
</template>

<script lang="ts" setup>
	import rollVue from '../../components/roll.vue';
	import { onBeforeMount, reactive, ref } from 'vue';
	import img1 from './assets/1.png'
	import img2 from './assets/2.png'
	import img3 from './assets/3.png'
	import img4 from './assets/4.png'
	import { storeToRefs } from 'pinia';
	import { useMore_imgs } from '../../store';
	import router from '../../router';
	let content = ref('')

	const usemore = useMore_imgs()
	const { head_more_list, Content } = storeToRefs(usemore)
	const { GetMore } = usemore
	let img_list = reactive([
		img1,
		img2,
		img3,
		img4
	])
	onBeforeMount(() => {
		GetMore()
	})
	const search = () => {
		Content.value = content.value
		// console.log(Content.value)
		router.push('/more')
	}
</script>

<style scoped>
	.common-layout {
		min-width: 2000px;
		max-width: 2000px;
		display: flex;
		background: linear-gradient(to bottom, #bccf90 0%, #EAD6EE 40%);
		z-index: 1;
		position: relative;
		left: 20px;
		top: 20px;
		gap: 10px;
		border:  1p solid ;
		box-shadow: 15px 20px 10px #cdcdcd; 
	}

	#header {
		min-width: 1000px;
	}

	#title1 {
		display: flex;
		position: relative;
		left: 665px;
		top: 150px;
		width: 300px;
		background: linear-gradient(to right, #100d12, #5a201d);
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		color: linear-gradient();
		font-weight: 800;
		font-size: 40px;
	}

	#title2 {
		display: flex;
		position: relative;
		left: 735px;
		top: 200px;
		width: 100px;
		background: linear-gradient(to right, #a359ff, #ff9131);
		-webkit-background-clip: text;
		-webkit-text-fill-color: transparent;
		color: linear-gradient();
		font-weight: 900;
		font-size: 30px;
	}

	#head-box {
		display: flex;
		position: relative;
		left: 500px;
		top: 250px;
		width: 600px;
	}

	#head-search {
		width: 550px;
		height: 50px;
		border-radius: 13px;
	}

	#head-botton {
		position: relative;
		left: -90px;
		top: 9px;
		width: 85px;
		height: 38px;
		border-radius: 8px;
	}

	.el-main {
		position: relative;
		top: 800px;
		min-height: 1215px;
		max-width: 2050px;
		z-index: 1;
		box-shadow: 15px 20px 10px #cdcdcd; 
		background: linear-gradient(to bottom, #EAD6EE 0%, #f4d7b1 50%);
	}

	#head-main-box1 {
		display: flex;
		position: relative;
		top: 50px;
		left: 80px;
		min-width: 1500px;
		max-width: 1600px;
	}

	#head-main-box1-span1 {
		position: relative;
		left: 25px;
		top: -70px;
		color: #f88a31;
		font-weight: bold;
		font-size: 30px;
	}

	#head-main-box1-span2 {
		position: relative;
		left: 25px;
		top: -65px;
		color: #ed927a;
		font-size: 18px;
	}

	#head-main-box1-card {
		position: relative;
		left: -60px;
		margin-right: 50px;
	}

	#img1 {
		width: 250px;
		height: 250px;
	}

	#head-main-box2 {
		display: flex;
		position: relative;
		top: 180px;
		left: 80px;
		min-width: 1500px;
		max-width: 1500px;
	}

	#head-main-box2-span1 {
		position: relative;
		top: -65px;
		font-size: 16px;
		color: #f89be3;
	}

	#head-main-box2-span2 {
		position: relative;
		top: -60px;
		font-weight: bold;
		font-size: 30px;
		color: #f87ff9;
	}

	#head-main-box2-card {
		width: 240px;
		height: 240px;
		position: relative;
		left: -68px;
		margin-right: 26px;
		margin-bottom: 10px;
	}

	#img2 {
		position: relative;
		top: -20px;
		left: -20px;
		width: 240px;
		height: 240px;
	}
	#head_bottom1 {
		position: relative;
		display: flex;
		height: 0px;
	}
	#head_bottom2 {
		display: flex;
		position: relative;
		top: -165px;
		left: -20px;
		background: #e9e0d9;
		min-width: 2000px;
		max-width: 100%;
		height: 537px;      
		z-index: 2;
	}
	#head_bottom3{
		display: flex;
		position: relative;
		left: 770px;
		top: 5px;
		width: 100px;
		height: 50px;
		border-radius: 30px;
	}
	
</style>