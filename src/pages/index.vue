<template>
	<div class="index-wrap">
		<div class="index-left">
			<div class="index-left-block">
				<h2>全部产品</h2>
				
				<template v-for="product in productList">
					<h3>{{ product.title }}</h3>
					<ul>
						<li v-for="item in product.list">
							<a :href="item.url">{{ item.name }}</a>
							<span v-if="item.hot" class="hot-tag">HOT</span>
						</li>
					</ul>
					<div v-if="!product.last" class="hr"></div>
				</template>
			</div>
			<div class="index-left-block lastest-news">
				<h2>最新消息</h2>
				<ul>
					<li v-for="item in newsList">
						<a :href="item.url" class="new-item">{{ item.title }}</a>
					</li>
				</ul>
			</div>
		</div>
		<div class="index-right">
		<slide-show :slides="slides" :inv="invTime"></slide-show>	
			<div class="index-board-list">
				<div class="index-board-item" v-for="(item, index) in boardList" :class="[{'line-last': index % 2 !==0}, 'index-board-' + item.id]">
					<div class="index-board-item-inner">
						<h2>{{ item.title }}</h2>
						<p>{{ item.description }}</p>
						<div class="button">
							<router-link :to="{path: 'detail/' + item.toKey}">立即购买</router-link>
						</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	import slideShow from '../components/slideShow'
	export default {
		components: {
			slideShow
		},
		created () {
			this.$http.get('api/getNewsList').then((res) => {
				this.newsList = res.data;
			},(err) => {
				console.log(err);
			});
			this.$http.get('api/getBoardList').then((res) => {
				this.boardList = res.data;
			}, (err) => {
				console.log(err);
			});
			this.$http.get('api/getProductList').then((res) => {
				this.productList = res.data;
			}, (err) => {
				console.log(err);
			})
			
		},
		data () {
			return {
				invTime: 2000,
				slides: [
					{
          				src: require('../assets/slideShow/pic1.jpg'),
          				title: 'xxx1',
        				href: 'detail/analysis'
        			},
        			{
            			src: require('../assets/slideShow/pic2.jpg'),
          				title: 'xxx2',
          				href: 'detail/count'
       				},
					{
          				src: require('../assets/slideShow/pic3.jpg'),
          				title: 'xxx3',
        				href: 'http://xxx.xxx.com'
        			},
        			{
        				src: require('../assets/slideShow/pic4.jpg'),
          				title: 'xxx4',
          				href: 'detail/forecast'
        			}
        		],
				boardList: [],
				newsList: [],
				productList: {}
			}
		}
	}
</script>

<style scoped>
	.index-wrap {
		width: 1200px;
		margin: 0 auto;
		overflow: hidden;
	}

	.index-left {
		float: left;
		width: 300px;
		text-align: left;
	}

	.index-right {
		float: left;
		width: 900px;
	}

	.index-left-block {
		margin: 15px;
		background-color: #fff;
		box-shadow: 0 0 1px #ddd;
	}

	.index-left-block .hr {
		margin-bottom: 20px;
	}

	.index-left-block h2 {
		padding: 10px 15px;
		margin-bottom: 20px;
		color: #fff;
		background-color: #4fc08d;
	}

	.index-left-block h3 {
		padding: 0 15px 5px;
		font-weight: bold;
		color: #222;
	}

	.index-left-block ul {
		padding: 10px 15px;
	}

	.index-left-block ul li{
		padding: 5px;
	}

	.hot-tag {
		background-color: #f00;
		color: #fff;
	}

	.lastest-news {
		min-height: 512px;
	}

	.new-item {
		display: inline-block;
		width: 230px;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}

	.index-board-list {
		overflow: hidden;
	}

	.index-board-item {
		float: left;
		width: 400px;
		padding: 20px;
		margin: 0 20px 20px 0;
		box-shadow: 0 0 1px #ddd;
		background-color: #fff;
	}

	.line-last {
		margin-right: 0;
	}

	.index-board-item-inner {
		min-height: 125px;
		padding-left: 120px;
	}

	.index-board-earth .index-board-item-inner {
		background: url(../assets/images/1.png) no-repeat;
	}

	.index-board-loud .index-board-item-inner {
		background: url(../assets/images/3.png) no-repeat;
	}

	.index-board-car .index-board-item-inner {
		background: url(../assets/images/2.png) no-repeat;
	}

	.index-board-hill .index-board-item-inner {
		background: url(../assets/images/4.png) no-repeat;
	}

	.index-board-item h2 {
		margin-bottom: 15px;
		font-size: 18px;
		font-weight: bold;
		color: #000;
	}

	.button {
		margin-top: 20px;
	}
</style>