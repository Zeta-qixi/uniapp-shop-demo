<template>
	<view>

	</view>
</template>

<script>
	export default {
		data() {
			return {

				providerList: [],
				data: [],
				detailDec: ""
			}
		},
		onLoad(option) {

			let data = JSON.parse(decodeURIComponent(option.data));
			console.log(data)

		},
		
		methods: {
			
		}
	}
</script>

<style>

</style>
