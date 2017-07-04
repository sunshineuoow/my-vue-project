<template>
	<div class="detail-wrap">
		<div class="detail-left">
			<div class="product-board">
				<img :src="productIcon">
				<ul>
					<router-link v-for="item in products" :to="{ path: item.path }" tag="li" active-class="active" key="item.icon">
						{{ item.name }}
					</router-link>	
				</ul>
			</div>
		</div>
		<div class="detail-right">
			<keep-alive>
				<router-view></router-view>
			</keep-alive>
		</div>
	</div>
</template>

<script>
	export default {
		data () {
			return {
				products:[
					{
        			  name: '数据统计',
        			  path: 'count',
        			  icon: require('../assets/images/3.png'),
        			  active: false
        			},
        			{
        			  name: '数据预测',
        			  path: 'forecast',
        			  active: false
        			},
        			{
        			  name: '流量分析',
        			  path: 'analysis',
        			  active: false
        			},
        			{
        			  name: '广告发布',
        			  path: 'publish',
        			  active: false
        			}
				],
				imgMap: {
    			    '/detail/analysis': require("../assets/images/1.png"),
    			    '/detail/forecast': require("../assets/images/2.png"),
    			    '/detail/count': require("../assets/images/3.png"),
    			    '/detail/publish': require("../assets/images/4.png")
    			}
			}
		},
		computed: {
			productIcon () {
				return this.imgMap[this.$route.path]
			}
		}
	}
</script>

<style>
	.detail-wrap {
		width: 1200px;
		margin: 0 auto;
		padding-top: 20px;
		overflow: hidden;
	}

	.detail-left {
		float: left;
		width: 200px;
		text-align: center;
	}

	.detail-right {
		float: left;
		width: 980px;
		margin-left: 20px;
	}

	.product-board {
		padding: 20px 0;
		background-color: #fff;
	}

	.product-board ul {
		margin-top: 20px;
	}

	.product-board ul li {
		padding: 10px 15px;
		text-align: left;
		cursor: pointer;
	}

	.product-board li.active,
	.product-board li:hover {
		background-color: #4fc08d;
		color: #fff;
	}

	.product-board li a {
		display: block;
	}

	.sales-board {
		background-color: #fff;
	}

	.sales-board-intro h2 {
		padding: 20px;
		font-size: 20px;
	}

	.sales-board-intro p {
		line-height: 1.8;
		padding: 10px 20px;
		color: #999;
		background-color: #f7fcff;
	}

	.sales-board-form {
		padding: 30px 20px;
		font-size: 14px;
	}

	.sales-board-line {
		clear: both;
		padding-bottom: 20px;
	}

	.sales-board-line-left {
		display: inline-block;
		width: 100px;
	}

	.sales-board-line-right {
		display: inline-block;
		width: 75%;
	}

	.sales-board-des {
		padding: 15px 20px;
		border-top: 20px solid #f0f2f5;
	}

	.sales-board-des h2 {
		padding-bottom: 15px;
		font-size: 20px;
	}

	.sales-board-des h3 {
		padding: 20px 0 10px;
		font-size: 18px;
		font-weight: bold;
	}

	.sales-board-des p {
		line-height: 1.6;
	}

	.sales-board-des li {
		padding: 5px 0;	
	}

	.sales-board-table {
		width: 100%;
		margin-top: 20px;
	}

	.sales-board-table th {
		color: #fff;
		background-color: #4fc08d;
	}

	.sales-board-table td {
		padding: 15px;
		border: 1px solid #f0f2f5;
	}
</style>