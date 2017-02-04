<style lang="scss">
	$text: 1rem;
	$size: 2rem;
	.block{
		display: inline-block;
		max-width: 200px;
		margin: 5px;
		flex-direction: column;
		position: relative;
		.count{
			display: flex;
			align-items: center;
			justify-content: center;
			position: absolute;
			top: 0;
			right: -$size/2 + 0.5rem;
			background: red;
			width: $size;
			height: $size;
			border-radius: 50%;
			font-size: 20px;
			color: white;
		}
		img{
			flex: 1;
			margin: 5px;
			width: 100%;
		}
		.name{
			font-size: $text;
			font-weight: 700;
		}
		.price{
			color: red;
		}
	}
	.order{
		display: flex;
		align-items: center;
		width: 100%;
		div{
			font-size: $text;
			border: 1px solid #999;
			border-radius:3px;
			margin: 2px;
			flex: 1;
			height: 1.5rem;
			display: flex;
			justify-content: center;
			align-items: center;
			cursor: pointer;
			user-select:none;
		}
	}
</style>

<template>
	<div class="block">
		<div class="count" v-if="count != 0">{{ count }}</div>
		<img :src="img || 'https://martin-upload.b0.upaiyun.com/web/2017/02/4cb4a876a19277c786af8614074ab05a.jpg'" alt="">
		<div class="name">{{ num + ' ' + name }}</div>
		<div class="price">{{ '￥' + price }}</div>
		<div class="order">
			<div @click="half">半</div>
			<div @click="add">+</div>
			<div @click="minus">-</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'list',
	data() {
		return {
			count: 0,
		};
	},
	props: ['num', 'name', 'img', 'price'],
	methods: {
		add() {
			this.$parent.price = Number(this.$parent.price) + Number(this.price);
			this.count += 1;
			this.addToOrder();
		},
		minus() {
			if (this.count !== 0) {
				if (this.count === 0.5) {
					this.count = 0;
					this.$parent.price = Number(this.$parent.price) - Number(this.price / 2);
					this.addToOrder(true);
					return;
				}
				this.count -= 1;
				this.$parent.price = Number(this.$parent.price) - Number(this.price);
				this.addToOrder(true);
			}
		},
		half() {
			this.$parent.price = Number(this.$parent.price) + Number(this.price / 2);
			this.count += 0.5;
			this.addToOrder(false, true);
		},
		addToOrder(must, half) {
			if (((this.count !== 1 || half) && this.count !== 0.5) || must) {
				this.$parent.order.forEach((items, i) => {
					if (items.name === this.name) {
						if (this.count === 0) {
							this.$parent.order.splice(i, 1);
							return;
						}
						this.$parent.order[i].count = this.count;
						return;
					}
				});
				return;
			}
			this.$parent.order.push({
				name: this.name,
				count: this.count,
				price: this.price,
				number: this.num,
			});
		},
	},
};
</script>