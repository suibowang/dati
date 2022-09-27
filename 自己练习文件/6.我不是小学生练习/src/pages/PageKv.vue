<template>
	<div class="kv">
		<!-- <div>123456</div> -->
		<div>
			<div class="kv-title-wp">
				<div class="kv-title1"></div>
				<div class="kv-title2"></div>
			</div>
			<div class="kv-desk-wp" >
				<div class="kv-desk-rank"></div>
				<div class="kv-desk-start scaleIt" @click="showNext()"></div>
				<div class="kv-desk-store"></div>
				<div class="kv-desk-my"></div>
			</div>
		</div>	
    </div>
</template>
<style lang="less" >
	img{
		width: 625px;
		height: 417px;
	}
	// .zhu{
	// 	top: 50%;
	// 	margin-top: -333.5px;
	// 	position: absolute;
	// 	width: 750px;
	// 	height: 1334px;
	// 	border: 1px solid gold;
	// 	// background-color: blueviolet;
	// }
	.kv{
		position: relative;
		width: 100vw;
		height: 100vh;
        .bg('../assets/pagekvImg/2.jpg');
	}
	.bg(@url){
		background-image:url(@url);
	    background-size: cover;
		background-repeat: no-repeat;
	}
	.kv-title-wp {
	  position: absolute;
	  width: 100vw;
	}
	.kv-title2 {
		top: 129px;
		left: 54px;
		width: 625px;
		height: 417px;
		position: absolute;
	  .bg('../assets/pagekvImg/2-6.png');
	}
	.kv-title1 {
		top:78px;
		left: 145px;
		width: 394px;
		height: 88px;
		position: absolute;
	  // top: 78px;
	  // position: absolute;
	  // margin-left: -199px;
	  // left: 50vw;
	  // width: 398px /* 398/16 */;
	  // height: 89px /* 89/16 */;
	  .bg('../assets/pagekvImg/2-1.png');
	}
	.kv-desk-wp {
	  position: absolute;
	  top: 57vh;
	  width: 750px /* 750/16 */;
	  height: 569px /* 575/16 */;
	  .bg('../assets/pagekvImg/2-3.png');
	}
	.kv-desk-rank {
	  position: absolute;
	  left: 0;
	  width: 201px /* 201/16 */;
	  height: 175px /* 175/16 */;
	  background-image: url(../assets/pagekvImg/2-4.png);
	  background-size: cover;
	  background-repeat: no-repeat;
	}
	.kv-desk-start {
	  position: absolute;
	  left:219px ;
	  width:312px /* 315/16 */;
	  height:204px/* 208/16 */;
	  background-image: url(../assets/pagekvImg/2-2.png);
	  background-size: cover;
	  background-repeat: no-repeat;
	}
	.kv-desk-store {
	  position: absolute;
	  left:547px ;
	  width:160px /* 315/16 */;
	  height: 138px/* 208/16 */;
	  background-image: url(../assets/pagekvImg/2-5.png);
	  background-size: cover;
	  background-repeat: no-repeat;
	}
	.kv-desk-my{
		position: absolute;
		left:460px ;
		top: 275px;
		width:199px /* 315/16 */;
		height: 142px/* 208/16 */;
		background-image: url(../assets/pagekvImg/2-7.png);
		background-size: cover;
		background-repeat: no-repeat;
	}
	.scaleIt {
	  animation: scaleIt 1s ease-in-out infinite both;
	}
	@keyframes scaleIt {
	  0%, 100% {
	    transform: scale(1);
	  }
	  50% {
	    transform: scale(1.1);
	  }
	}
</style>
<script setup>
	const emit = defineEmits(['nextPage'])
	// const props = defineProps({
	// 	Obj:Object
	// })
	console.log("23")

	function showNext (){
		emit('nextPage','isPOShow')
	}
</script>