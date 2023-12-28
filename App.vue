<script>
	export default {}
</script>

<style lang="scss">
	/*每个页面公共scss */
	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}
	
	.mar{
		height: 4vh;
	}

	li {
		list-style: none;
		border-radius: 24rpx;
	}

	input {
		font-family: Microsoft YaHei, Heiti SC, tahoma, arial, Hiragino Sans GB, "\5B8B\4F53", sans-serif;
	}

	input {
		border: 0;
		;
		outline: none;
	}

	.hide,
	.none {
		display: none;
	}

	.clearfix:after {
		visibility: hidden;
		clear: both;
		display: block;
		content: ".";
		height: 0
	}

	@import 'uni_modules/uview-ui/index.scss';
</style>