<template>
	<div class="order-wrap">
		<h3>您的产品</h3>
		<div class="order-list-choose">
			<div class="order-list-option">
				选择产品
				<v-selection
				:selections="products"
				@on-change="productChange"></v-selection>
			</div>

			<div class="order-list-options">
				开始日期:
			</div>

			<div class="order-list-options">
				结束日期:
			</div>

			<div class="order-list-options">
				关键词:
				<input type="text" class="order-query" name="keyword">
			</div>
		</div>
		<div class="order-list-table">
			<table>
				<tr>
					<th></th>
				</tr>
				<tr>
					<td></td>
				</tr>
			</table>
		</div>
	</div>
</template>

<script>
	import VSelection from '../components/base/selection'

	export default {
		components: {
			VSelection,
		},
		data () {
			return {
				products: [
        			{
        			  	label: '数据统计',
        			  	value: 0
        			},
        			{
        			  	label: '数据预测',
        			  	value: 1
        			},
        			{
        			  	label: '流量分析',
        			 	value: 2
        			},
        			{
        			  	label: '广告发布',
        			  	value: 3
       				}
				],
			}
		},
		methods: {
			productChange () {
				
			}
		}
	}
</script>

<style scoped>
	
</style>