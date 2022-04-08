<template>
  <div>
    <div class='container'>
    <div class="game">
					<button :class="className" id='blue'  v-on:click="addClass" type="button" class="game__field game__field-blue"></button>
					<button :class="className" id='red' v-on:click="addClass" type="button" class="game__field game__field-red"></button>
					<button :class="className" id='yellow' v-on:click="addClass" type="button" class="game__field game__field-yellow"></button>
					<button :class="className" id='green' v-on:click="addClass" type="button" class="game__field game__field-green"></button>
		</div>
  <div class="info">
					<div class="info__button">
						<button v-on:click="gameStart" type="button">Start</button>
					</div>
					<div class="info__lostAlert"></div>
					<div class="info__radio radio">
						<h2>Game Options:</h2>
						<div class="radio__container">
							<input type="radio" id="easy" name="level" value="легкий">
							<label for="easy">Легкий</label>
						</div>
						<div class="radio__container">
							<input type="radio" id="medium" name="level" value="средний" checked>
							<label for="medium">Средний</label>
						</div>
						<div class="radio__container">
							<input type="radio" id="hard" name="level" value="сложный">
							<label for="hard">Сложный</label>
						</div>
					</div>
				</div>
        </div>
  </div>
</template>

<script>


let array=[];
let userPick = [];


export default {
  name: 'App',
  components: {
  },
  
  data(){
    return{
      className:'',
      roundNum: '',
    }
  },
  methods:{
    addClass(e) {
      e.target.classList.add('active')
      setTimeout(()=>e.target.classList.remove('active'),200)
      if(e.target.classList.contains('game__field-blue')){
        userPick.push(1);
        audio.play();
        console.log(userPick);
        compare();
      }else if(e.target.classList.contains('game__field-red')){
        userPick.push(2);
        audio2.play();
        console.log(userPick);
        compare();
      }else if(e.target.classList.contains('game__field-yellow')){
        userPick.push(3);
        audio3.play();
        console.log(userPick);
        compare();
      }else if(e.target.classList.contains('game__field-green')){
        userPick.push(4);
        audio4.play();
        console.log(userPick);
        compare();
      }
    },
  
    gameStart(){
      array=[];
      game(array);
      changeLevel();
    },
    
  },

}


function getRandom(min,max){
    min= Math.ceil(min);
    max=Math.floor(max);
    return Math.floor(Math.random() * (max-min))+min;
}






function game(array){
    array.push(getRandom(1,5));
    array.forEach(function(item, i, array){
      setTimeout(function(){
    if(item === 1){
      console.log(i)
      console.log(array);
      let blueF= document.getElementById('blue');
      blueF.classList.add('active');
      audio.play();
      setTimeout(()=>blueF.classList.remove('active'),200);
    }else if(item===2){
      console.log(i)
      console.log(array);
      let redF= document.getElementById('red');
      redF.classList.add('active');
      audio2.play();
      setTimeout(()=>redF.classList.remove('active'),200);
    }else if(item===3){
      console.log(i)
      console.log(array);
      let yellowF= document.getElementById('yellow');
      yellowF.classList.add('active');
      audio3.play();
      setTimeout(()=>yellowF.classList.remove('active'),200);
    }else if(item===4){
      console.log(i)
      console.log(array);
      let greenF= document.getElementById('green');
      greenF.classList.add('active');
      audio4.play();
      setTimeout(()=>greenF.classList.remove('active'),200);
    }
    },choosenLevel * ++i)
    userPick=[]
    })
}

function compare(){
    if(array.length !== 0){
        for(let i=0;i<=userPick.length-1;i++){
            if(array[i] == userPick[i]){
                if(JSON.stringify(array)==(JSON.stringify(userPick))){
                    game(array);
                }
            }else{
                alert('Игра окончена!')
                array=[];
            }
        }
    }
}

let choosenLevel;
function changeLevel(){
    let radio = document.getElementsByName('level');
    for(let i=0; i< radio.length;i++){
        if(radio[i].checked ){
            if(radio[0].checked){
                choosenLevel = 1500;
                console.log(choosenLevel)
            }else if(radio[1].checked){
                choosenLevel = 1000;
                console.log(choosenLevel)
            }else if(radio[2].checked){
                choosenLevel = 400;
                console.log(choosenLevel)
            }
        }
    }
}






import sound from './/assets/sounds/sounds_1.mp3'
import sound2 from './/assets/sounds/sounds_2.mp3'
import sound3 from './/assets/sounds/sounds_3.mp3'
import sound4 from './/assets/sounds/sounds_4.mp3'

const audio = new Audio(sound)
const audio2 = new Audio(sound2)
const audio3 = new Audio(sound3)
const audio4 = new Audio(sound4)


</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.game {
    display: flex;
    width: 302px;
    height: 296px;
    position: relative;
    flex-wrap: wrap;
    box-shadow: 4px 4px 8px 0px rgba(34, 60, 80, 0.2);
    border-radius: 100%;

}
.game__field-red{  background-color: red;
        opacity: 0.5;
        width: 145px;
        height: 145px;
        border-top-right-radius:100%;
        border-right: 3px solid transparent;
        border-top: 3px solid transparent;}
.game__field-blue{  background-color: blue;
        opacity: 0.5;
        width: 149px;
        height: 145px;
        border-top-left-radius: 100%;
        border-left: 3px solid transparent;
        border-top: 3px solid transparent;}
.game__field-yellow{  background-color: yellow;
        opacity: 0.5;
        width: 149px;
        height: 145px;
        border-bottom-left-radius: 100%;
        border-left: 3px solid transparent;
        border-bottom: 3px solid transparent;
        margin-bottom: 6px;}
.game__field-green{  background-color: green;
        opacity: 0.5;
        width: 145px;
        height: 145px;
        border-bottom-right-radius: 100%;
        border-right: 3px solid transparent;
        border-bottom: 3px solid transparent;}

.game__field-red:hover,
.game__field-blue:hover,
.game__field-yellow:hover,
.game__field-green:hover{
border-color: black;
}
.container{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    align-items: center;
    margin-top: 60px;

}
.info{
    width: 300px;
    height: 300px;
    padding-left: 50px;
}
.info__button{
  width: 100px;
  height: 50px;
  background-color: #6DABE8;
  border-radius: 50%;
  margin-left: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}
.info__round{
  font-size: 30px;
}
.info__lostAlert{
  margin-top: 20px;
}

.radio{
    display: flex;
    flex-direction: column;
    margin-top: 30px;
}
.radio__container{
  display: flex;
  margin-top: 10px;
  align-items: center;
}
.radio__container input{
  width: 50px;
  height: 20px;
  align-self: center;
}


.active{
    opacity: 1;
}

h1{
    text-align: center;
    font-size: 40px;
    margin-top: 20px;
    font-weight: bold;
}
h2{
    font-size: 20px;
    font-weight: bold;
}
input,
button,
textarea {
	border: none;
	font-size: inherit;
}
input::-ms-clear {
	display: none;
}
button {
	cursor: pointer;
	background-color: inherit;
}
.info__button:hover{
  background-color: blue;
 
}
@media(max-width: 666px){
.info{
  width: auto;
  padding-left:0 ;
}
}
</style>
