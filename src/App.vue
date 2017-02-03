<template>
	<div id="app">
		<!-- <img src="./assets/logo.png"> -->
		<div class="final_price">{{ '总价 ￥' + price }}</div>
		<div class="order_list" >
			<list v-for="items in menu" :num="items.number" :name="items.name" :img="items.img" :price="items.price"></list>
		</div>
		<div class="blank"></div>
		<div @click="show_order" class="show_order btn">结算</div>
		<MaskShadow v-show="show_mask">
			<div v-show="show_mask" class="ordered">
				{{ order }}
			</div>
		</MaskShadow>
	</div>
</template>

<script>
import MaskShadow from './components/mask';
import List from './components/list';
import Json from './assets/menu.json';

export default {
	name: 'app',
	components: {
		List, MaskShadow,
	},
	data() {
		return {
			menu: Json,
			price: 0,
			order: [],
			show_mask: false,
		};
	},
	methods: {
		show_order() {
			this.show_mask = true;
		},
	},
};
</script>

<style lang="scss">
@import "style/common.css";
#app {
	font-family: 'Avenir', Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
	position: relative;
	.final_price{
		width: 100%;
		height: 40px;
		position: fixed;
		background: rgba(0,0,0,0.7);
		top: 0;
		font-size: 30px;
		line-height: 40px;
		color: white;
		z-index: 1;
	}
}
.order_list{
	width: 100%;
}
.blank{
	height:40px;
}
.show_order{
	color:white;
	background: rgba(200,100,111,0.8);
	position: fixed;
	bottom:5px;
	right:5px;
	height: 40px;
	line-height: 40px;
	width:100px;
}
.ordered{
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%,-50%);
	width:80%;
	height:80%;
	background:white;
	color: black;
}
</style>
