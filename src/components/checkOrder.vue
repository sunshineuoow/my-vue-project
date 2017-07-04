<template>
	<div>
		<this-dialog :is-show="isShowCheckDialog" @on-close="checkStatus">
			<p>请检查你的支付状态</p>
			<div class="button" @click="checkStatus">支付成功</div>
			<div class="button" @click="checkStatus">支付失败</div>
		</this-dialog>
		<this-dialog :is-show="isShowSuccessDialog" @on-close="toOrderList">
			购买成功!
		</this-dialog>
		<this-dialog :is-show="isShowFailDialog" @on-close="toOrderList">
			购买失败!
		</this-dialog>
	</div>
</template>

<script>
	import Dialog from './base/dialog'

	export default {
		components: {
			thisDialog: Dialog
		},
		props: {
			isShowCheckDialog: {
				type: Boolean,
				defalut: false
			},
			orderId: {
				type: [String, Number]
			}
		},
		data () {
			return {
				isShowSuccessDialog: false,
				isShowFailDialog: false
			}
		},
		methods: {
			toOrderList () {
				// this.isShowFailDialog = false;
				// this.isShowSuccessDialog = false;
				console.log(1);
				this.$router.push({path: '/orderList'});
			},
			checkStatus () {
				this.$http.post('/api/checkOrder', {orderId: this.orderId}).then( (res) => {
					this.isShowSuccessDialog = true;
					this.$emit('on-close-check-dialog');
				}, (err) => {
					this.isShowFailDialog = true;
					this.$emit('on-close-check-dialog');
				})
			}
		}
	}	
</script>

<style scoped>
	
</style>