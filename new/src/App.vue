<script setup>
	import navigtionVue from './components/navigtion.vue';
</script>

<template>
	<navigtionVue></navigtionVue>
	<div id="app-box"><router-view/></div>

</template>

<style>
	#app-box{
		background-color: #f7f7f7;
		min-height: 2000px;
		height: 100vh;
		width: 100vw;
	}
</style>
