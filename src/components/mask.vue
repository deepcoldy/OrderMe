<style lang="scss" scoped>
	.mask{
		position:fixed;
		top:0;
		left:0;
		width:100%;
		height:100%;
		z-index:2;
		background-color:rgba(0,0,0,0.8);
	}
</style>
<template>
	<div class="mask" @click.self="close">
		<transition name="slideUp">
			<slot></slot>
		</transition>
	</div>
</template>
<script>
export default {
	data() {
		return {
			move_height: '',
			move_speed: '',
		};
	},
	components: {
	},
	mounted() {
	},
	methods: {
		close() {
			this.$parent.show_mask = false;
		},
	},
};
</script>