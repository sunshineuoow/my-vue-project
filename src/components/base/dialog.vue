<template>
	<div>
		<div class="dialog-wrap">
			<div class="dialog-cover" v-if="isShow" @click="closeMyself"></div>
			<transition name="drop">			<div class="dialog-content" v-if="isShow">
					<p class="dialog-close" @click="closeMyself">x</p>
					<slot>empty</slot>
				</div>
			</transition>
		</div>
	</div>
</template>

<script>
	export default {
		props: {
			isShow: {
				type: Boolean,
				default: false
			}
		},
		data () {
			return {}
		},
		methods: {
			closeMyself () {
				this.$emit('on-close');
			}
		}
	}
</script>

<style scoped>
/*动画*/
	.drop-enter-active {
		transition: all .5s ease;
	}
	.drop-leave-active {
		transition: all .3s ease;
	}
	.drop-enter {
		transform: translateY(-500px);
	}
	.drop-leave {
		transform: translateY(-500px);
	}

/*样式*/
	.dialog-wrap {
		position: fixed;
		width: 100%;
		height: 100%;
	}
	.dialog-cover {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-color: #000;
		opacity: .3;
		z-index: 5;
	}
	.dialog-content {
		position: fixed;
		top: 20%;
		left: 50%;
		width: 50%;
		max-height: 50%;
		margin-left: -25%;
		padding: 2%;
		border: 2px solid #464068;
		line-height: 1.6;
		background-color: #fff;
		z-index: 10;
		overflow: auto;
	}
	.dialog-close {
		position: absolute;
		top: 5px;
		right: 5px;
		width: 20px;
		height: 20px;
		text-align: center;
		cursor: pointer;
	}
	.dialog-close:hover {
		color: #4fc08d;
	}
</style>