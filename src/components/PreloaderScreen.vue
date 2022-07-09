<template>
<transition name="fade">
	<div v-if="show" class="preloader">
		<h1>Загрузка...</h1>
	</div>
</transition>
</template>

<script>
export default {
	name: 'PreloaderScreen',
	data(){
		return {
			show: true
		}
	},
	mounted(){
		if(this.show) this.showToggle()
	},
	methods: {
		showToggle(){
			setTimeout(() => {
				this.show = false
			}, 1500)
		}
	}
}
</script>

<style>

.preloader {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	position: absolute;
	width: 100%;
	height: 100%;
	background-color: white;
	z-index: 9999;
}
.h1 {
  font-family: "Source Sans Pro";
  font-style: normal;
		margin-top: 1rem;
    }
</style>