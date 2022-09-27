<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import Loading from './pages/Loading.vue'
import PageKv from './pages/PageKv.vue'
import PageOne from './pages/PageOne.vue'
import {reactive,ref,shallowRef,markRaw} from 'vue'
// const Obj=reactive({
// 	isLDShow:true,
// 	isKVShow:false,
// 	isPOShow:false,
	
// })
const abc = reactive({
	isLDShow:markRaw(Loading),
	isKVShow:markRaw(PageKv),
	isPOShow:markRaw(PageOne),
})
console.log(PageOne)
const celect = reactive({
	 tabComp:Loading
})
function onNextShow(para){
		// Object.keys(Obj).map((item)=>{
		// 	Obj[item] = false
		// }),
		// Obj[para]=true	
		celect.tabComp = abc[para]
		console.log(celect.tabComp)
	}

</script>

<template>
	<div>
	<transition name="route" mode="out-in" appear >
		<component :is="celect.tabComp" @nextPage="onNextShow"></component>
	</transition>
	</div>
</template>
<style lang="less">
	.route-enter-from {
	  opacity: 0;
	  transform: translateY(50vh);
	  position: absolute;
	}
	.route-enter-active {
	  transition: all 0.5s ease-out; 
	}
	.route-leave-to {
	  opacity: 0;
	  transform: translateY(-50vh);
	  position: absolute;
	  
	}
	.route-leave-active {
	  transition: all 0.5s ease-in; 
	}

</style>
