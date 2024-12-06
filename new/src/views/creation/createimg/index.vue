<template>
	<div class="common-layout">
		<el-container>
			<el-aside width="400px">
				<el-card id="card1">
					<div id="card-box1">
						<span>
							图片生成(未完善)
						</span>
					</div>
					<div id="card-box2">
						<span id="card-box2-span">需求描述</span>
						<el-card shadow="hover" style="width: 360px;height: 200px">
							<el-input v-model="text"
								style="width: 360px;height: 200px;position: relative;left: -20px;top: -20px;"
								maxlength="50" placeholder="您可以进行描述:" show-word-limit type="text" clearable
								class=" demo_input" />
						</el-card>
					</div>
					<div id="card-box3">
						<span id="card-box3-span">图片参考</span>
						<el-card>
							<el-upload class="avatar-uploader" action="" :show-file-list="false"
								:on-success="handleAvatarSuccess" :before-upload="beforeAvatarUpload">
								<img v-if="imageUrl" :src="imageUrl" class="avatar" />
								<el-icon v-else class="avatar-uploader-icon">
									<Plus />
								</el-icon>
							</el-upload>
						</el-card>
					</div>
					<div id="card-box4">
						<el-button type="primary" @click="onSubmit" id="card-box4-button">一键生成</el-button>
					</div>
				</el-card>
			</el-aside>
			<el-main>
				<el-card id="card2">
					<el-card shadow="hover" id="card2-box">
						<img src='../../assets/can.png' id="demo_img1" />
					</el-card>
				</el-card>
			</el-main>
		</el-container>
	</div>
</template>

<script lang="ts" setup>
	import { ref } from 'vue';
	import { useCreate_imgs } from '../../../store';
	import { storeToRefs } from 'pinia';
	import { ElMessage } from 'element-plus'
	import { Plus } from '@element-plus/icons-vue'

	import type { UploadProps } from 'element-plus'

	const imageUrl = ref('')
	const useimg = useCreate_imgs()
	let { Create_list } = storeToRefs(useimg)
	let { CreateImg, Del } = useimg
	let text = ref()
	let key = ref(1)
	const onSubmit = () => {
		let data = text.value
		let url = imageUrl.value
		CreateImg({ data, url })
		key.value = 0
	}
	const del = () => {
		Del()
		key.value = 1
	}
	const handleAvatarSuccess : UploadProps['onSuccess'] = (
		response,
		uploadFile
	) => {
		imageUrl.value = URL.createObjectURL(uploadFile.raw!)
		console.log(imageUrl.value)
	}
	const beforeAvatarUpload : UploadProps['beforeUpload'] = (rawFile) => {
		if (rawFile.type !== 'image/jpeg') {
			ElMessage.error('Avatar picture must be JPG format!')
			return false
		} else if (rawFile.size / 1024 / 1024 > 2) {
			ElMessage.error('Avatar picture size can not exceed 2MB!')
			return false
		}
		return false
	}
</script>

<style scoped>
	.common-layout{
		position: relative;
		top: 10px;
		left: 10px;
	}
	#card1 {
		border-radius: 20px;
		display: flex;
		height: 620px;
	}
	.el-aside{
		box-shadow: 5px 10px 5px #d7d4d1;
	}
	#card-box1 {
		position: relative;
		top: -10px;
		left: 105px;
	}

	#card-box2 {
		position: relative;
		top: 10px;
	}

	#card-box2-span {
		display: flex;
		margin-bottom: 10px;
	}

	#card-box3 {
		position: relative;
		top: 30px;
	}

	#card-box3-span {
		display: flex;
		margin-bottom: 10px;
	}

	#card-box4 {
		position: relative;
		margin-top: 10px;
		top: 45px;
		left: 11.5px;
	}

	#card-box4-button {
		display: flex;
		width: 340px;
	}

	.avatar-uploader .avatar {
		width: 178px;
		height: 178px;
		display: block;
	}

	.avatar-uploader {
		position: relative;
		left: -0px;
		top: -0px;
	}
	#card2{
		display: flex;
		min-width: 180px;
		max-width: 2000px;
	}
	#card2-box{
		display: flex;
		display: inline-block;
		margin-right: 15px;
		margin-bottom: 10px;
		width: 100px;
		height: 100px;
	}
	#demo_img1{
		position: relative;
		left: -20px;
		top: -20px;
		width: 100px;
		height: 100px;
	}
</style>
<style>
	.avatar-uploader .el-upload {
		border: 1px dashed var(--el-border-color);
		border-radius: 6px;
		cursor: pointer;
		position: relative;
		overflow: hidden;
		transition: var(--el-transition-duration-fast);
	}

	.avatar-uploader .el-upload:hover {
		border-color: var(--el-color-primary);
	}

	.el-icon.avatar-uploader-icon {
		font-size: 28px;
		color: #8c939d;
		width: 318px;
		height: 160px;
		text-align: center;
	}
</style>