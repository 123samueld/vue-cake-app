<template>
<section id="updateCakeSection" class="sectionBackgrounds">
<!-- Modal View -->
<div v-if="confirmUpdateCheck" class="createAndUpdateModals" id="updateModal">
<h1>Cake updated</h1>
<button @click="confirmUpdateModalFunc(), reloadEvent()">OK</button>
</div>

<div v-if="displayUpdateValidateYum" class="createAndUpdateModals">
<h1>Please choose a Yum Factor between 1 and 5.</h1>
<button @click="confirmUpdateModalFunc">OK</button>
</div>

<div class="updateCakeBox centralBox" id="updateCakeBox"  v-if="displayUpdateBox">
<h2>Update</h2>
<select 
	name="updateCakesList" 
	id="updateCakesList" 
	class="inputFields" 
	v-model="updateCakeSelection"
	>

<option value="" disabled selected>Select...</option>
<option 
v-for="(cake, index) in cakes" 
:key="index"
:value="cake.id"
>{{cake.name}}</option>

</select>
<form id="updateForm" @submit.prevent>
<input 
    type="number" 
    name="updateYum" 	
	id="updateYum"
	class="inputFields" 
	min="1" 
	max="5"
	placeholder="Yum Factor..."
	v-model="updateCakeYumFactor">
<textarea
	name="updateReview" 
	id="updateReview" 
	class="inputFields inputTextField"
	placeholder="Update Review..."
	rows="5" 
	cols="60"
	v-model="updateCakeReview">
</textarea>
<button 
	type="button"
	id="updateButton"  
	:disabled="!updateFormValid"
	@click="confirmUpdateModalFunc(), 
	sendUpdateRequest()"
	>Update 
	<i class="fa fa-pencil"></i>
</button>
</form>
</div>
</section>
</template>

<script>
import axios from 'axios';
export default {
props: [
"reload"
],
emits: [
"update"
],
data(){
return{
cakes: '',
displayUpdateValidateYum: false,
confirmUpdateCheck: false,
confirmUpdate: false,
cancelUpdate: false,
displayUpdateBox: true,

updateCakeSelection: '',
updateCakeYumFactor: '',
updateCakeReview: '',
configGet: {
method: 'get',
url: 'https://samuel-davidson.co.uk/mmmDelicous/backend/rBja6258CxqhFHxT/readSSEP.php'
},
url: 'https://samuel-davidson.co.uk/mmmDelicous/backend/rBja6258CxqhFHxT/updateSSEP.php/',
};
},
methods: {
getUpdateData(){
axios(this.configGet)
.then(response => (this.cakes = response.data))
.then(response => console.log(response));
},
updateHasData: function(value){
if(value.length > 0){
return true;
}else{
return false;
}
},
confirmUpdateModalFunc: function() {
this.displayUpdateBox = !this.displayUpdateBox;
if(this.updateCakeYumFactor == "1" ||
this.updateCakeYumFactor == "2" ||
this.updateCakeYumFactor == "3" ||
this.updateCakeYumFactor == "4" ||
this.updateCakeYumFactor == "5"){
	this.confirmUpdateCheck = !this.confirmUpdateCheck;
}else{
	this.displayUpdateValidateYum = !this.displayUpdateValidateYum; 
}
},
cancelUpdateFunc: function(){
	this.confirmUpdateCheck = !this.confirmUpdateCheck;
	this.cancelUpdate = !this.cancelUpdate;
},
sendUpdateRequest(){
axios({ 
method: 'put',
url: 'https://samuel-davidson.co.uk/mmmDelicous/backend/rBja6258CxqhFHxT/updateSSEP.php',
data: {
id: this.updateCakeSelection,
yumFactor: this.updateCakeYumFactor,
comment: this.updateCakeReview,
},
headers : {
"Access-Control-Allow-Headers": "Content-Type",
"Access-Control-Allow-Origin": "*",
"Access-Control-Allow-Methods": "*",
},
})
.then(res => console.log(res))
.catch(e => console.log(e.response));
},
reloadEvent(){
this.$emit("update", true)
}
},
computed: {
updateFormValid: function(){
if(
this.updateHasData(this.updateCakeSelection) &&
this.updateHasData(this.updateCakeYumFactor) &&
this.updateHasData(this.updateCakeReview)
){
return true;
}else{
return false;
}
},
},
mounted(){
this.getUpdateData();
console.log("Update page remounted");
}
};
</script>

<style>
*{
    padding: 0;
    margin: 0;
}
#updateCakeSection{
background-image: url("../assets/images/reviewsI.jpg");
border-top: 0.5px solid #fffdd0;
}
/* Update section box */
.updateCakeBox{
height: 85vh;
width: 84%;
}
.updateCakeBox h2{
margin-bottom: 0;	
}
#updateYum{
z-index: 0;
}
textarea{
text-align: left; 
justify-content: left;
font-family: hominFun;
}
.updateCakeBox option{
font-size: 0.25em;
}
/* Update Section Form Yum Factor */
.updateYum{
height: 200px;
width: 800px;
font-size: 5em;
}
.updateReview{
height: 200px;
width: 800px;
font-size: 5em;
}
.updateCakeBox button{
position: relative;
top: 60px;
}
/* XL Phone and up */
@media only screen and (min-device-width : 450px){
#updateForm{
top: -180px;
}
.inputTextField{
height: 20vh;
text-align: none;
}
#updateButton{
top: 25px;
}
}
/* Tablet and up */
@media only screen and (min-device-width : 600px){
#updateCakeSection{
background-image: url("../assets/images/reviewsII.jpg");
}
#updateCakeBox{
top: -22px;
}
#updateForm{
top: -50px;
}
.updateCakeBox select{
margin-top: -8vh;
}
.updateCakeBox option{
font-size: 0.5em;
}
}
/* M Tablet and up */
@media only screen and (min-device-width : 750px){
.centralBox{
width: 50%;
}
#updateButton{
top: 50px;
}
}
/* L Tablet and up */
@media only screen and (min-device-width : 1000px){
#updateCakeSection{
background-image: url("../assets/images/reviews.jpg");
}
.centralBox option{
font-size: 0.9em;
}
.inputFields{
border-radius: 15px 0;
}
#updateCakesList{
width: 55vw;
}
}
@media only screen and (min-device-width : 1300px){
#updateForm{
top: 15px;
}
#updateCakesList{
margin-top: 2vh;
width: 40vw;
}
#updateButton{
top: 0;
}
}
</style>