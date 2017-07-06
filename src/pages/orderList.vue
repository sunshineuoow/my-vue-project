<template>
	<div class="order-wrap">
		<h3>您的产品</h3>
		<div class="order-list-choose">
			<div class="order-list-options">
				选择产品
				<v-selection
				:selections="products"
				@on-change="productChange"></v-selection>
			</div>

			<div class="order-list-options">
				开始日期:
				<date-picker :value="startDate"></date-picker>
			</div>

			<div class="order-list-options">
				结束日期:
				<date-picker :value="endDate"></date-picker>
			</div>

			<div class="order-list-options">
				关键词:
				<input type="text" class="order-query" name="keyword">
			</div>
		</div>
		<div class="order-list-table">
			<table>
				<tr>
					<th v-for="head in tableHeads" :class="{active: head.active}"
					@click="changeOrderType(head)">{{ head.label }}</th>
				</tr>
				<tr v-for="item in tableData" :key="item.period">
					<td v-for="head in tableHeads">{{ item[head.key] }} </td>
				</tr>
			</table>
		</div>
	</div>
</template>

<script>
	import VSelection from '../components/base/selection'
	import DatePicker from 'vue-date-picker'
	import _ from 'lodash'

	export default {
		components: {
			VSelection,
			DatePicker
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
				tableHeads: [
    			    {
    			      	label: '订单号',
    			      	key: 'orderId'
    			    },
    			    {
    			      	label: '购买产品',
    			      	key: 'product'
    			    },
    			    {
    			      	label: '版本类型',
    			      	key: 'version'
    			    },
    			    {
    			      	label: '有效时间',
    			      	key: 'period'
    			    },
    			    {
    			      	label: '购买日期',
    			      	key: 'date'
    			    },
    			    {
    			      	label: '数量',
    			      	key: 'buyNum'
    			    },
    			    {
    			      	label: '总价',
    			      	key: 'amount'
    			    }
    			],
    			startDate: '',
    			endDate: '',
    			// tableData: [],
    			currentOrder: 'asc'
			}
		},
		computed: {
			tableData () {
				return this.$store.getters.getOrderList
			}
		},
		methods: {
			productChange (obj) {
				this.$store.commit('updatePramrs', {
					key: 'productId',
					val: obj.value
				})
				// this.productId = obj.value;
				// this.getList();s
			},
			getList () {
				let reqParams = {
					query: this.query,
					productId: this.productId,
					startDate: this.startDate,
					endDate: this.endDate
				}
				this.$http.post('/api/getOrderList', reqParams).then( (res) => {
					this.tableData = res.data.list;
				}, (err) => {
					
				})
			},
			changeOrderType (headItem) {
				this.tableHeads.map((item) => {
					item.active = false;
					return item
				})
				headItem.active = true;
				if(this.currentOrder === 'asc'){
					this.currentOrder = 'desc';
				} else if (this.currentOrder === 'desc') {
					this.currentOrder = 'asc'
				}
				this.tableData = _.orderBy(this.tableData, headItem.key, this.currentOrder)
			}
		},
		mounted () {
			// this.getList();
			this.$store.dispatch('fetchOrderList');
		}
	}
</script>

<style scoped>
	.order-wrap {
		width: 1200px;
		min-height: 800px;
		margin: 20px auto;
		overflow: hidden;
	}

	.order-wrap h3 {
		font-size: 20px;
		font-weight: bold;
		margin-bottom: 20px;
	}

	.order-query {
		height: 25px;
		line-height: 25px;
		border: 1px solid #e3e3e3;
		outline: none;
		text-indent: 10px;
	}

	.order-list-options {
		display: inline-block;
		padding-left: 15px;
	}

	.order-list-options:first-child {
		padding-left: 0;
	}

	.order-list-table {
		margin-top: 20px;
	}

	.order-list-table table {
		width: 100%;
		background-color: #fff;
	}

	.order-list-table th,
	.order-list-table td {
		padding: 10px 0;
		border: 1px solid #e3e3e3;
		text-align: center;
	}

	.order-list-table th {
		border: 1px solid #4fc08d;
		color: #fff;
		background-color: #4fc08d;
		cursor: pointer;
	}

	.order-list-table th.active {
		background-color: #35495e;
	}
</style>