<template>
	<div>
		<div class="app-header">
			<div class="app-header-inner">
				<!-- <router-link :to="{path:'/'}"> -->
					<img src="../assets/logo.png">
				<!-- </router-link> -->
				<div class="header-nav">
					<ul class="nav-list">
						<li>{{ username }}</li>
						<li v-if="username !== ''" class="nav-pile">|</li>
						<li v-if="username !== ''">退出</li>
						<li v-if="username === ''" @click="logClick">登录</li>
						<li class="nav-pile">|</li>
						<li>注册</li>
						<li class="nav-pile">|</li>
						<li @click="aboutClick">关于</li>
					</ul>
				</div>
			</div>
		</div>
		<div class="app-content">
			<keep-alive>
				<router-view></router-view>
			</keep-alive>
		</div>
		<div class="app-footer">
			<p>&copy; 2016 fishenal MIT</p>
		</div>

		<my-dialog :is-show="isShowAboutDialog" @on-close="closeDialog('isShowAboutDialog')">
			<p>本报告在调研数据的基础上，采用定性与定量相结合的方式深入分析了专车市场发展的驱动因素与阻碍因素、专车市场背后的产业格局、专车企业的竞争格局、用户对专车市场的依赖程度、专车对其他交通工具运力的补充效应等，通过这五个章节的研究反映专车市场的发展态势和面临的问题。报告力求客观、深入、准确地反映中国专车市场发展情况，为政府、企事业单位和社会各界提供决策依据。 </p>
		</my-dialog>

		<my-dialog :is-show="isShowLogDialog" @on-close="closeDialog('isShowLogDialog')">
			<log-form @has-log="onSuccessLog"></log-form>
		</my-dialog>
	</div>
</template>

<script>
	import Dialog from './base/dialog'
	import LogForm from './logForm'

	export default{
		name: 'layout',
		components: {
			MyDialog: Dialog,
			LogForm,
		},
		data() {
			return {
				isShowAboutDialog: false,
				isShowLogDialog: false,
				username: ''
			}
		},
		methods: {
			aboutClick () {
				this.isShowAboutDialog = true;
			},
			logClick () {
				this.isShowLogDialog = true;
			},
			closeDialog (attr) {
				this[attr] = false
			},
			onSuccessLog (data) {
				this.closeDialog('isShowLogDialog');
				this.username = data.username
			}
		}
	}
</script>

<style>
/* http://meyerweb.com/eric/tools/css/reset/ 
   v2.0 | 20110126
   License: none (public domain)
*/

html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed, 
figure, figcaption, footer, header, hgroup, 
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font-size: 100%;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure, 
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
ol, ul {
  list-style: none;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
a {
  color: inherit;
  text-decoration: none;
}
body {
  background: #f0f2f5;
  font-family: "Helvetica Neue",Helvetica,Arial,"Hiragino Sans GB","Hiragino Sans GB W3","Microsoft YaHei UI","Microsoft YaHei","WenQuanYi Micro Hei",sans-serif;
  font-size: 14px;
  color: #444;
}

.app-header {
	width: 100%;
	height: 90px;
	line-height: 90px;
	color: #b2b2b2;
	background-color: #363636;
}

.app-header-inner {
	width: 1200px;
	margin: 0 auto;
}

.app-header-inner img{
	width: 50px;
	margin-top: 20px;
}

.header-nav {
	float: right;
}

.nav-list {
	overflow: hidden;
}

.nav-list li{
	float: left;
	cursor: pointer;
}

.nav-pile {
	padding: 0 10px;
}

.app-footer{
	width: 100%;
	height: 80px;
	line-height: 80px;
	margin-top: 30px;
	background-color: #e3e4e8;
	text-align: center;
	clear: both;
}

.app-content {
	width: 1200px;
	margin: 0 auto;
}

.hr {
	width: 100%;
	height: 1px;
	background-color: #ddd;
}

.g-form-line {
	padding: 15px 0;
}

.g-form-label {
	display: inline-block;
	width: 100px;
	font-size: 16px;
}

.g-form-input {
	display: inline-block;
}

.g-form-input input {
	width: 200px;
	height: 30px;
	line-height: 30px;
	padding: 0 10px;
	border: 1px solid #ccc;
	vertical-align: middle;
}

.g-form-btn {
	padding-left: 100px;
}

.g-form-error {
	padding-left: 15px;
	color: red;
}

.button {
	display: inline-block;
	padding: 10px 20px;
	color: #fff;
	background-color: #4fc08d;
	cursor: pointer;
}
</style>