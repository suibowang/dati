<template>
	<div>
	<div class="po"  >
		<div class="test-clock">
			<span class="text-num">{{Obj.tihao}}/5</span>
			<span class="text-desc">答题进度</span>
		</div>
		<div class="text-bb">
			<div class="text-black">第{{Obj.datalist[Obj.tihao].num}}题</div>
			<div :class="Obj.choose!=''?'test-question-hide' : 'test-question'"> {{Obj.datalist[Obj.tihao].que}}</div>
		</div>
		<div class="test-desk">
			 <div class="opt-wp">
				  <div class="opt-wp1" @click="chooseDa('a')">
				  <div class="option opta">
				             <div class="text">{{Obj.datalist[Obj.tihao].a.txt}}</div>
				             <div class="judge1" v-show="Obj.choose==='a'&&Obj.datalist[Obj.tihao].a.isRight===0"></div>
				            <div class="judge2" v-show="Obj.choose==='a'&&Obj.datalist[Obj.tihao].a.isRight===1"></div>
				           </div>
				</div>	
				<div class="opt-wp2" @click="chooseDa('b')">
				  <div class="option opta">
				             <div class="text">{{Obj.datalist[Obj.tihao].b.txt}}</div>
				           <div class="judge1" v-show="Obj.choose==='b'&&Obj.datalist[Obj.tihao].b.isRight===0"></div>
				           <div class="judge2" v-show="Obj.choose==='b'&&Obj.datalist[Obj.tihao].b.isRight===1"></div>
				           </div>
				</div>	
				<div class="opt-wp3" @click="chooseDa('c')">
				  <div class="option opta">
				             <div class="text">{{Obj.datalist[Obj.tihao].c.txt}}</div>
				            <div class="judge1" v-show="Obj.choose==='c'&&Obj.datalist[Obj.tihao].c.isRight===0"></div>
				            <div class="judge2" v-show="Obj.choose==='c'&&Obj.datalist[Obj.tihao].c.isRight===1"></div>
				           </div>
				</div>	
				<div class="opt-wp4" @click="chooseDa('d')">
				  <div class="option opta">
				             <div class="text">{{Obj.datalist[Obj.tihao].d.txt}}</div>
				            <div class="judge1" v-show="Obj.choose==='d'&&Obj.datalist[Obj.tihao].d.isRight===0"></div>
				            <div class="judge2" v-show="Obj.choose==='d'&&Obj.datalist[Obj.tihao].d.isRight===1"></div>
				           </div>
				</div>	
			 </div>
		</div>
	</div>
	<div class="pop-wp" v-show="Obj.isPopShow">
		<div class="pop-camera1">
			<div class="pop-shadow"></div>
		</div>
		<div class="pop-pos pop-pos-dis">
			<img :src="imgSrc" alt="" class="pop-dis-img">
			<p class="pop-text">本次答对题目<span class="pop-num">{{Obj.achievement}}</span>道</p>
			<div class="pop-result">
			    <div class="pop-coin">+{{100*Obj.achievement}}</div>
			</div>
			    <div class="pop-btn" @click="replay"></div>
		</div>
		 <div class="pop-camera2"></div>
	</div>
	</div>
</template>

<script setup>
	import { questions } from '../questions.js';
    import {reactive,ref,shallowRef,markRaw,onMounted,toRaw,onUpdated,computed} from 'vue'
	const emit = defineEmits(['nextPage'])
	function showNext (){
		emit('nextPage','isLDShow')
	}
	const Obj = reactive({
		datalist:[],
		tihao:1,
		choose:'',
		achievement:0,
		isPopShow:false,
		dizhi:'pop-pos1'
		
	})
	const imgSrc = computed(()=>new URL(`../assets/pageoneImg/${Obj.dizhi}.png`, import.meta.url).href)
	Obj.datalist = questions
	function  fnPos() {
	      switch (Obj.achievement) {
	        case 0:
	        case 1:
		     return Obj.dizhi='pop-pos1'
	        case 2:
			 return Obj.dizhi='pop-pos2'
	        case 3:
			 return Obj.dizhi='pop-pos3'
	        case 4:
			 return Obj.dizhi='pop-pos4'
	        case 5:
			 return Obj.dizhi='pop-pos5'
	        default:
			 return Obj.dizhi='pop-pos1'
	      }
		  }
	function chooseDa(pac){
		if(Obj.tihao>=5){
			if(Obj.choose===''){
				Obj.choose=pac
				if(Obj.datalist[Obj.tihao][pac].isRight===1){
								  Obj.achievement+=1
			}
				fnPos()
				Obj.isPopShow=true
		}}
		else{
		    if(Obj.choose===''){
			  Obj.choose=pac
			  if(Obj.datalist[Obj.tihao][pac].isRight===1){
				  Obj.achievement+=1
				  console.log(Obj.achievement)
			  }
			  setTimeout(function () {
			        Obj.choose=''
					Obj.tihao+=1
			      },300);	
		}}
	}
	function replay(){
		// Obj.achievement = 0
		// Obj.tihao = 1
		// Obj.choose = ''
		// Obj.isPopShow = false
        window.location.reload()
	}

</script>

<style lang="less" scoped>
	.abc{
		width: 100px;
		height: 100px;
		background-image: url(../assets/pageoneImg/pop-pos1.png);
	}
	.po{
		position: relative;
		width: 100vw;
		height: 100vh;
	    .bg('../assets/pageoneImg/bg.png')
	}
	.bg(@url){
		background-image:url(@url);
	    background-size: cover;
		background-repeat: no-repeat;
	}
	.test-clock{
		position: absolute;
        left: 20px;
		top: 21px;
		width: 711px;
		height: 128px;
		 .bg('../assets/pageoneImg/test-clock.png')
	}
	.text-num{
		position: absolute;
		left: 31px;
		top: 12px;
		line-height: 100px;
		text-align: center;
		font-size: 40px;
		color: #d63b44;
		display: inline-block;
		 font-weight: bold;
	}
	.text-desc{
		position: absolute;
		left: 150px;
		top: 20px;
		color: #235c7f;
		display: inline-block;
		font-weight: bold
	}
	.text-bb{
		position: absolute;
		top: 164px;
		left: 20px;
		width: 711px;
		height: 568px;
		text-align: center;
		.bg('../assets/pageoneImg/text-bb.png')	
	}
	.text-black{
		position: absolute;
		top: 83px;
		left: 143px;
		width: 461px;
		height: 99px;
		color: #0d1a3e;
		font-size: 50px;
		text-align: center;
		line-height: 99px;
		color: #333;
		.bg('../assets/pageoneImg/text-black.png')	
	}
	.test-question {
	  position: absolute;
	  top: 230px /* 230/16 */;
	  width: 100%;
	  box-sizing: border-box;
	  padding: 0 2rem;
	  text-align: center;
	  font-size: 1.2rem;
	  color: white;
	  transition: opacity .3s ease-in;
	}
	.test-question-hide {
	  opacity: 0;
	}
	.test-desk{
		position: absolute;
		bottom: 0px;
		width: 750px;
		height: 540px;
		.bg('../assets/pageoneImg/test-desk.png')	
	}
    .opt-wp{
	top: 15px;
	position: absolute;
    }
	.opt-wp1{
		left:50px;
		position: absolute;
		width:305px;
		height: 150px;
		font-size: 35px;
		transform: rotate(-10deg);
	}
	.opt-wp2{
		position: absolute;
		width:305px;
		height:150px;
		left: 400px;
		font-size: 35px;
		transform: rotate(4deg);
	}
	.opt-wp3{
		top: 170px;
		position: absolute;
		width:305px;
		height: 150px;
		left: 50px;
		font-size: 35px;
	}
	.opt-wp4{
		top: 170px;
		position: absolute;
		width:305px;
		height: 150px;
		left: 400px;
		font-size: 35px;
	}
	.option{
		position: absolute;

		width:305px;
		height: 150px;
		text-align: center;
		line-height: 150px;
		.bg('../assets/pageoneImg/opt-wp.png')	
	}
	.judge1 {
	  position: absolute;
	  right: 20px;
	  bottom:30px;
	  width: 86px;
	  height: 61px /* 61/16 */;
	  background-image: url('../assets/pageoneImg/error.png');
	  background-size: cover;
	  background-repeat: no-repeat;
	}
	 .judge2 {
	  position: absolute;
	  right: 20px;
	  bottom:30px;
	  width: 86px;
	  height: 61px /* 61/16 */;
	  background-image: url('../assets/pageoneImg/right.png');
	  background-size: cover;
	  background-repeat: no-repeat;
	}
	.pop-wp{
		 position: fixed;
		  left: 0;
		  right: 0;
		  top: 0;
		  bottom: 0;
		  background-color: rgba(0, 0, 0, .6);
		
	}
	.pop-camera1 {
	  left: 30px;
	  position: absolute;
	  width: 689px /* 689/16 */;
	  height: 325px;
	  .bg('../assets/pageoneImg/pop-camera1.png');
	  z-index: 5;
	}
	.pop-camera2 {
	  position: absolute;
	  left:30px;
	  top: 325px;
	  width: 689px /* 689/16 */;
	  height: 64px /* 64/16 */;
	  .bg('../assets/pageoneImg/pop-camera2.png');
	}
	.pop-shadow {
	  position: absolute;
	  bottom: -32px;
	  left: 50px;
	  width: 587px /* 587/16 */;
	  height: 36px /* 36/16 */;
	  background-image: url(../assets/pageoneImg/pop-shadow.png);
	  background-size: cover;
	  background-repeat: no-repeat;
	}
	.pop-pos {
	  position: absolute;
	  top: 320px;
	  left: 95px;
	  width: 17.5rem /* 280/16 */;
	  padding: .625rem /* 10/16 */;
	  box-sizing: border-box;
	  background-color: #fff;
	  z-index: 3;
	  img {
	    width: 521px /* 521/16 */;
	    height: 620px /* 620/16 */;
	  }
	}
	.pop-text {
	  margin-top: 32px;
	  font-size: 32px;
	  text-align: center;
	  line-height: 1.2;
	}
	.pop-result {
	  margin: 32px 0;
	  display: flex;
	  align-items: center;
	  justify-content: center;
	}
	.pop-coin {
	  padding-left: 60px;
	  background-image: url(../assets/pageoneImg/pop-coin.png);
	  background-repeat: no-repeat;
	  background-size: auto 100%;
	  font-weight: bold;
	  font-size: 40px;
	  color: #e50e45;
	  }
.pop-btn {
  margin: 0 auto;
  width: 237px /* 237/16 */;
  height:83px /* 83/16 */;
  background-image: url(../assets/pageoneImg/pop-btn.png);
  background-size: cover;
  background-repeat: no-repeat;
  transition: transform .3s ease, opacity .2s ease;
  &:active {
    opacity: .8;
    transform: scale(.9);
  }
}
.poster {
  display: none;
  position: fixed;
  left: 0;
  top: 0;
  width: 100vw;
  height: 500px /* 500/16 */;
  opacity: 0;
  z-index: 10;
  transform: translateZ(0);
}
.popbounce {
  animation:  display 2s popbounce .2s forwards;
}
@keyframes popbounce {
  from {
    opacity: 0;
    transform: translateY(-10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.pop-pos-dis {
  animation: display 1s .2s ease-out both;
}

@keyframes display {
  from {
    transform: translateY(-100%);
  }
  to {
    transform: translateY(0);
  }
}

</style>