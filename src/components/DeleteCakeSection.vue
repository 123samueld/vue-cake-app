<template>
<section id="deleteCakeSection" class="sectionBackgrounds">
<!-- Modal View -->
<div v-if="confirmDelete" class="deleteModal">
<h1>Cake deleted</h1>
<button @click="confirmDeleteModalFunc(), reloadEvent()">OK</button>
</div>

<div class="deleteCakeBox centralBox" id="deleteCakeBox" v-if="displayDeleteBox">
<h2>Delete</h2>
<select 
  name="deleteCakesList" 
  id="deleteCakesList" 
  class="inputFields"
  v-model="deleteCakeSelection"
>
<option value="" disabled selected>Select...</option>
<option
    v-for="(cake, index) in cakes" 
    :key="index"
    :value="cake.id"
    >{{cake.name}}</option>
</select>
<button 
    id="deleteButton" 
    :disabled="!deleteFormValid"
    @click="confirmDeleteModalFunc(), 
    sendDeleteRequest()">
    Delete
    <i class="fa fa-trash"></i>
</button>
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
updated: false,
cakes: null,
cake: null,
review: 'confirm',

deleteCakeSelection: '',

confirmDelete: false,
displayDeleteBox: true,

reloadCheck: this.reload,

config: {
method: 'get',
url: 'https://samuel-davidson.co.uk/mmmDelicous/backend/rBja6258CxqhFHxT/readSSEP.php'
},
url: 'https://samuel-davidson.co.uk/mmmDelicous/backend/rBja6258CxqhFHxT/deleteSSEP.php/',
};
},
methods: {
getDeleteData(){
axios(this.config)
.then(response => (this.cakes = response.data))
.then(response => console.log(response));
},

deleteHasData(){
if(this.deleteCakeSelection > 0){
return true;
}else{
return false;
}
},

confirmDeleteModalFunc() {
this.confirmDelete = !this.confirmDelete;
this.displayDeleteBox = !this.displayDeleteBox;
},

sendDeleteRequest(){
axios.delete(this.url + this.deleteCakeSelection)
.then(res => console.log(res))
.catch(e => console.log(e.response));
},

reloadEvent(){
this.$emit("update", true)
}

},
computed: {
deleteFormValid() {
if(this.deleteHasData(this.deleteCakeSelection)) {
return true;
}else{
return false;
}
}
},
mounted(){
this.getDeleteData();
}
};
</script>

<style>
*{
    padding: 0;
    margin: 0;
}
#deleteCakeSection{
background-image: url("../assets/images/crumbsI.jpg");
scroll-snap-align: start;
border-top: 0.5px solid #fffdd0;

}
.deleteCakeBox{
height: 70vh;
width: 84%;
}
#deleteCakeBox{
top: 80px;
}
.deleteCakeBox select{
margin-top: -100px;
}
.deleteCakeBox button{
position: relative;
top: 100px;
}

/* Modal View */
.deleteModal{
position: relative;
margin-right: auto;
margin-left: auto;
text-align: center;
background: rgba(255, 255, 255, 0.25);
border-radius: 100px 0px;
top: 80px;
height: 70vh;
width: 84%;
}

.deleteModal h1, button{
position: relative;
top: 30vh;
font-family: hominFun;
font-size: 2rem;
}
.deleteModal button{
position: relative;
top: 35vh;
width: 20vw;
font-size: 1.5rem;
}

/* XL Phone and up */
@media only screen and (min-device-width : 450px){
.deleteModal{
top: 62px;
height: 70vh;
width: 80%;
}
#deleteCakeBox{
top: 62px;
height: 70vh;
width: 80%;
}
#deleteCakeBox button{
top: 20vh;
} 
}
/* Tablet and up */
@media only screen and (min-device-width : 600px){
#deleteCakeSection{
background-image: url("../assets/images/crumbsIII.jpg");
}
.deleteModal{
top: 60px;
height: 70vh;
width: 78%;
}
#deleteCakeBox{
top: 26px;
height: 70vh;
width: 78%;
border-radius: 100px 0;
}
.deleteCakeBox h2{
margin-top: 5vh;
}
.updateCakeBox h2{
margin-top: 12vh;
font-size: 5em;
}
.deleteCakeBox select{
margin-top: -10vh;
width: 50vw;
}
.deleteCakeBox option{
font-size: 0.5em;
}
}
/* M Tablet and up */
@media only screen and (min-device-width : 750px){
.deleteModal{
width: 69%;
}
#deleteCakeBox{
width: 69%;
}
}
/* L Tablet and up */
@media only screen and (min-device-width : 1000px){
#deleteCakeSection{
background-image: url("../assets/images/crumbsII.jpg");
}
.deleteCakeBox{
top: 20px;
height: 90vh;
width: 50%;
}
.deleteCakeBox select{
width: 40vw;
}
.centralBox option{
font-size: 0.9em;
}
.inputFields{
border-radius: 15px 0;
}
#deleteCakesList{
width: 55vw;
}
}
@media only screen and (min-device-width : 1300px){
.deleteModal{
top: 62px;
width: 50%;
}
.deleteModal h1{
font-size: 2.5rem;
}
#deleteCakeBox{
width: 50%;
}
#deleteCakeBox select{
margin-top: 3vh;
}
#deleteCakesList{
width: 40vw;
}
#deleteButton{
top: 100px;
}
}
</style>