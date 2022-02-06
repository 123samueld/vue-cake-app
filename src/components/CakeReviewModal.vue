<template>
  <div class="modalView">
    <button @click="closeModal" > X </button>
    <div class="modalContentContainer">
    <img :src="info.imageUrl" id="cakeImg">
    <h1>{{info.name}}</h1>
    <table>
			<tr>
				<td v-for="n in parseInt(info.yumFactor)" :key="n"><img src="../assets/images/yum.png"></td>
				<td v-for="i in (5 - parseInt(info.yumFactor))" :key="i"><img src="../assets/images/yumBW.png"></td>
			</tr>
		</table>
    <p>{{info.comment}}</p>
  </div>
  </div>
</template>


<script>
export default {
props: ['info'],
data(){
  return{
    modalInfo: '',
  }
},
methods: {
closeModal(){
this.$emit('exit', true)
}
}
};
</script>

<style scoped>
.modalView{
z-index: 3;
position: fixed;
top: 0;
left: 0;
height: 100vh;
width: 100vw;
background-color: rgba(0, 0, 0, 0.75);
text-align: center;
}
.modalContentContainer{
position: relative;
top: -40px;
height: 90vh;
width: 90%;
margin: 0 5%;
border-radius: 50px 0;
border: 3px solid #000;
background-color: lightgray;
}
#cakeImg{
width: 70%;
margin-top: 10px;
}
h1{
font-size: 2rem;
font-family: hominFun;
}
table{
margin-top: -30px;
}
p{
margin-top: 10px;
font-size: 1.8rem;
font-family: hominFun;
}
button{
z-index: 12;
height: 70px;
width: 16%;
border-radius: 100%;
position: relative;
top: 88%;
margin: 0 42%;
}
@media only screen and (min-device-width : 450px){
table{
margin-top: -20px;
}
#cakeImg{
width: 59%;
}
}
@media only screen and (min-device-width : 600px){
#cakeImg{
width: 53%;
}
button{
width: 13%;
}
}
@media only screen and (min-device-width : 750px){
.modalContentContainer{
width: 80%;
margin: 0 10%;
border-radius: 80px 0;
}
#cakeImg{
width: 40%;
}
button{
width: 12%;
}
}
@media only screen and (min-device-width : 1000px){
.modalContentContainer{
width: 60%;
margin: 0 20%;
border-radius: 80px 0;
}
#cakeImg{
  width: 40%;
}
button{
height: 75px;
width: 75px;
}
}
@media only screen and (min-device-width : 1300px){
#cakeImg{
width: 35%;
}
}
@media only screen and (min-device-width : 1500px){
#cakeImg{
width: 30%;
}
}
</style>