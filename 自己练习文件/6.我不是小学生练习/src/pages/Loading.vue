<template>
	<div class="id" >
		<van-circle
		  v-model:current-rate="Obj.currentRate"
		  :rate="100"
		  :speed="100"
		  :text="Obj.loadingNum+'%'"
		  :clockwise="true"
		  :start-position='left'
		/>
	<!-- <div class="wrap">
		<div class="circle" ref="circle">
			<div class="percent left" :style="`transform: Obj.leftStyle}`" ref="left"></div>
			<div class="percent right wth0" ref="right"></div>
		</div>
		<div class="ld-bell"></div>
		<div class="num">
			<span>{{Obj.loadingNum}}%</span>
		</div>
	</div> -->
		<!-- <button @click="showNext()">Next</button> -->
	</div>
</template>

<script setup >
	import {reactive,ref} from 'vue';
	const Obj = reactive({
		leftStyle:'',
		loadingNum:0,
		currentRate:0
	})
	// const currentRate = 0
	const left = ref()
	const right = ref()
	const loading = setInterval(()=>{
	if(Obj.loadingNum>=100){
		
		
		showNext ()
	}
	else if(Obj.loadingNum>50){
	
	}
	Obj.loadingNum++
	},10)
	const emit = defineEmits(['nextPage'])
	function showNext (){
		emit('nextPage','isKVShow')
	}

</script>

<style lang="less" scoped>
	.id{
		width: 100vw;
		height: 100vh;
		display: flex;
		align-items: center;
        justify-content: center;
		flex-direction: column;
		background-size: contain;
		background-position-y: center;
		background-image: url(../assets/loadingImg/ld-bg.png);
		// background-repeat:no-repeat
		// width: 750px;
		// height: 1334px;
	}
	.ld-bell{
		width: 140px;
		height: 170px;
		background-image: url(../assets/loadingImg/ld-bell.png);
		background-size: cover;
		background-repeat: no-repeat;
	}
	.wrap,.circle,.percent{
		width: 130px;
		height: 130px;
		border-radius: 50%;
	}
	.circle, .percent {
	  position: absolute;
	}
	.wrap{
		position: relative;
		display: flex;
		align-items: center;
		justify-content: center;
        background-color: #fefefe;	
		}
	.percent{
			box-sizing: border-box;
		}
		.circle{
			box-sizing: border-box;
			clip: rect(0,130px,130px,65px);
		}
		.clip-auto{
			clip: rect(auto,auto,auto,auto);
		}
		.left{
			transition: transform ease;
			border: 64px solid #00b3ea;
			clip: rect(0,65px,130px,0px);
		}
		.right {
		  border: 4px solid #00b3ea;
		  clip: rect(0, 130px, 130px, 65px);
		}
		.wth0 {
		  width: 0;
		}
		.num {
		  margin-top: 10px /* 10/16 */;
		  margin-bottom: 96px;
		  font-size: 1rem;
		  line-height: 1.8;
		  text-align: center;
		}
</style>