<template>
<section id="cakesSection">
	<modal v-if="modalVisible" @exit="closeModal" :info="modalData"/>
	<ul>
    <li class="readCakeBox centralBox" id="readCakeBox" v-for="(cake, index) in cakes" :key="index">
		<img :src="cake.imageUrl">
		<h2>{{ cake.name }}</h2>
		<table>
			<tr>
				<td v-for="n in parseInt(cake.yumFactor)" :key="n"><img src="../assets/images/yum.png"></td>
				<td v-for="i in (5 - parseInt(cake.yumFactor))" :key="i"><img src="../assets/images/yumBW.png"></td>
			</tr>
		</table>
		<button id="openModalButton" class="openModalButton" @click="openModal(cake)">Review <i class="fa fa-comments"></i></button>
	</li>
	</ul>
</section>
</template>

<script>
import axios from 'axios';
import modal from './CakeReviewModal'
export default {
props: [
"reload"
],
components: {
modal
},

name: 'CakesSection',
data(){
return{
cakes: null,
cakeId: null,
nameProp: this.name,

reloadCheck: this.reload,

modalVisible: false,
modalData: null,
modalInfo: 'Some info here',

config: {
method: 'get',
url: 'https://samuel-davidson.co.uk/mmmDelicous/backend/rBja6258CxqhFHxT/readSSEP.php'
}
}
},
methods:{
getAPI(){
axios(this.config)
.then(response => (this.cakes = response.data))
.then(response => console.log(response));
},
openModal(data) {
this.modalData = data,
this.modalVisible = !this.modalVisible
},
closeModal(){
this.modalVisible = !this.modalVisible
},
},
mounted(){
this.getAPI();
}
}
</script>

<style>
#cakesSection{
background-image: url("../assets/images/loveDustI.jpg");
background-size: cover;
background-repeat: no-repeat;
height: 100vh;
}
#cakesSection ul{
width: 90vw;
margin: 0 5vw;
list-style: none;
display: inline-block;
overflow: auto;
overflow-y: hidden;
white-space: nowrap;
scroll-snap-type: x mandatory;
}
#cakesSection li{
display: inline-block;
scroll-snap-align: center;
margin: 0 50px 20px 50px;
}
#readCakeBox{
position: relative;
top: 12vh;
height: 95vh;
width: 84%;
}
img{
margin-top: 30px;
width: 80%;
height: 350px;
border-radius: 50px 0px;
margin-left: auto;
margin-right: auto;
}
#readCakeBox h2{
width: 100%;
background: white;
font-family: hominFun;
color: #000;
font-size: 2rem;
letter-spacing: 0;
}
table{
width: 200px;
margin-right: auto;
margin-left: auto;
}
table img{
width: 50px;
height: 50px;
}
.openModalButton{
font-family: hominFun;
}
.openModalButton:hover{
box-shadow: 0px 0px 20px 0px rgba(50, 50, 255, 0.75);}

#openModalButton{
top: 5px;
font-size: 2em;
height: 7vh;
width: 45vw;
}
/* XL Phone and up */
@media only screen and (min-device-width : 450px){
#cakesSection{
background-image: url("../assets/images/loveDustII.jpg");
}
#readCakeBox{
top: 10vh;
height: 94vh;
width: 84%;
margin: auto;
}
img{
margin-top: 2vh;
width: 250px;
height: 330px;
}
#readCakeBox h2{
margin-top: 2.5vh;
font-size: 2em;
}
table{
margin-top: -1.5vh;
margin-bottom: 2vh;
width: 55vw;
}
table img{
height: 7vh;
width: 8vw;
}
.openModalButton{
font-size: 3.5em;
height: 8vh;
width: 40vw;
}
}
/* Tablet and up */
@media only screen and (min-device-width : 600px){
#cakesSection{
background-image: url("../assets/images/loveDustIII.jpg");
}
#readCakeBox{
margin-top: none;
width: 65%;
border-radius: 50px 0;
}
img{
margin-top: 2vh;
width: 280px;
height: 350px;
}
#readCakeBox h2{
font-size: 2em;
}
table{
margin-top: -1vh;
margin-bottom: 1vh;
width: 45vw;
}
table img{
height: 6vh;
width: 6vw;
}
.openModalButton{
font-size: 3em;
height: 7vh;
width: 35vw;
}
}
/* M Tablet and up */
@media only screen and (min-device-width : 750px){
#readCakeBox{
top: 9vh;
height: 95vh;
width: 55%;
}
img{
margin-top: 2.5vh;
width: 260px;
height: 370px;
}
#readCakeBox h2{
font-size: 2em;
width: 90%;
margin-top: 0; 
}
table{
margin-top: 0;
margin-bottom: 2vh;
width: 30vw;
}
table img{
height: 7vh;
width: 6vw;
padding: 0 5px;
}
#openModalButton{
width: 30vw;
}
.fa-times{
font-size: 4em;
}
}
/* L Tablet and up */
@media only screen and (min-device-width : 1000px){
#cakesSection{
background-image: url("../assets/images/loveDust.jpg");
}
#readCakeBox{
margin-top: -4.5vh;
height: 95vh;
width: 40%;
margin: auto;
}
table{
margin-bottom: 1vh;
width: 20vw;
}
table img{
height: 5vh;
width: 3.5vw;
}
#openModalButton{
width: 22vw;
}
.fa-times{
font-size: 4em;
}
}
/* Laptop and up */
@media only screen and (min-device-width : 1300px){
#readCakeBox{
margin-top: -3vh;
height: 85vh;
width: 30%;
margin: auto;
}

#readCakeBox h2{
width: 100%;
font-size: 2rem;
}
table{
margin-top: -1vh;
margin-bottom: 1vh;
width: 20vw;
}
table img{
height: 6vh;
width: 3vw;
}
#openModalButton{
width: 18vw;
}
.fa-times{
font-size: 4em;
}
}
</style>