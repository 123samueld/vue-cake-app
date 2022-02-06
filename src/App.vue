<!-- Re-render compnents using Key -->
<!-- https://www.youtube.com/watch?v=bKHtLOV5F54 -->
<template>
<div  class="cookieConsent" v-if="activeCookieConsent">
  <h1>   This website uses delicious cookies. If you want more info please click 
    <span class="cookiePolicyViewLink"
      @click="toggleCookiePolicy()" 
      >
      here.
    </span>
  </h1>
  <button @click="closeCookieConsent(), closeSmallCookie()">OK</button>
</div>
<div class="cookiePolicyView" v-if="activeCookiePolicy">
    <div class="cookieBlockContainer">
      <h1>Cookies Policy</h1>
      <div class="cookieBlocks rightBlocks">
        <h2>What are Cookies?</h2>
        <p>Cookies are small files used to collect information about you and track your life in cyberspace.</p>
        <img src="./assets/images/cookiesView/cookieLectures.png" />
      </div>
      <div class="cookieBlocks leftBlocks">
        <h2>Are Cookies Safe?</h2>
        <p>Some very bad monsters collect all sorts of very personal data about you using Cookies.
        Those monsters might learn where you live, where you work, your likes and dislikes and what time you go to bed.  
        They make billions of dollars each year selling your private inforamtion to other greedy, power hungry monsters. 
        This information is often used to bombard you with political and commercial messaging until you give in and do what the monsters want.</p>
        <img class="monstersGallery"  src="./assets/images/cookiesView/wantedKorpCriminalsPoster.jpg" />
      </div>
      <div class="cookieBlocks rightBlocks">
        <h2>Should I Always Accept Cookies?</h2>
        <p>It's OK to not accept Cookies, quickly check the Cookie policy before accepting anything. This website only uses Cookies to check that people are visiting.
        No personal, intrusive information is collected or sold to monsters.</p>
        <img src="./assets/images/cookiesView/rejected.png" />
      </div>
      <div class="cookieBlocks leftBlocks">
        <h2>So, want a....</h2>
        <img src="./assets/images/cookiesView/wantACookie.png" />
      </div>
      <div class="buttons">
        <button @click="toggleCookiePolicy(), closeCookieConsent(), closeSmallCookie()">Yes</button>
        <button @click="oneSmallCookie()">No</button>
      </div>
    </div>
</div>  
<div  class="justOneSmallCookie" 
      :class="{active: isActive}"
      v-if="activeSmallCookie">
  <div class="smallCookieBox">
      <h2>Ok, no Cookie.</h2>
        <img src="./assets/images/cookiesView/noCookies.png" />
  </div>
</div>

 <div
    class="navbar" 
    :class="{navbarClosed: navbarClosed, navbarOpen: navbarOpen}"
    >
      <button @click="navbarToggle" class="navButton" id="navButton">
        <div
        class="slice"
          :class="{sliceI: sliceI, sliceITurn: sliceITurn}"></div>
        <div 
        class="slice"
          :class="{sliceII: sliceII, sliceIITurn: sliceIITurn}"></div>
        <div 
        class="slice"
          :class="{sliceIII: sliceIII, sliceIIITurn: sliceIIITurn}"></div>
      </button>
    <ul
      :class="{listClosed: listClosed, listOpen: listOpen}"
    >
      <li><a href="#landingSection" @click="navbarToggle">Welcome</a></li>
      <li><a href="#cakesSection" @click="navbarToggle">Cakes</a></li>
      <li><a href="#createCakeSection" @click="navbarToggle">Create Cake</a></li>
      <li><a href="#updateCakeSection" @click="navbarToggle">Update</a></li>
      <li><a href="#deleteCakeSection" @click="navbarToggle">Delete</a></li>
    </ul>
  </div>
  <div class="container">
    <LandingSection class="snapAlign" id="landingSection" />

    <CakesSection 
    class="snapAlign" 
    id="cakesSection" 
    :key="renderDeleteKey"
    />

    <CreateCakeSection 
    class="snapAlign" 
    id="createCakeSection"
    @update="updateData()"
    />

    <UpdateCakeSection 
    class="snapAlign" 
    id="updateCakeSection"
    @update="updateData()"
    :key="renderDeleteKey"
    />
    
    <DeleteCakeSection 
    class="snapAlign" 
    id="deleteCakeSection"
    @update="updateData()"
    :key="renderDeleteKey"

    />
  </div>

</template>

<script>
import LandingSection from './components/LandingSection.vue'
import CakesSection from './components/CakesSection.vue'
import CreateCakeSection from './components/CreateCakeSection.vue'
import UpdateCakeSection from './components/UpdateCakeSection.vue'
import DeleteCakeSection from './components/DeleteCakeSection.vue'



export default {
  name: 'App',
  components: {
    LandingSection,
    CakesSection,
    CreateCakeSection,
    UpdateCakeSection,
    DeleteCakeSection
  },
  data(){
    return{
      activeCookieConsent: true,
      activeCookiePolicy: false,
      activeSmallCookie: true,
      isActive: false,

      navbarClosed: true,
      navbarOpen: false,
      listOpen: false,
      listClosed: true,

      sliceI: true,
      sliceII: true,
      sliceIII: true,
      sliceITurn: false,
      sliceIITurn: false,
      sliceIIITurn: false,

      renderDeleteKey: 1
    }
  },
  methods: {
      navbarToggle(){
      this.navbarClosed = !this.navbarClosed;
      this.navbarOpen = !this.navbarOpen;
      this.listClosed = !this.listClosed;
      this.listOpen = !this.listOpen;
      this.sliceITurn = !this.sliceITurn;
      this.sliceIITurn = !this.sliceIITurn;
      this.sliceIIITurn = !this.sliceIIITurn;
      this.sliceI = !this.sliceI;
      this.sliceII = !this.sliceII;
      this.sliceIII = !this.sliceIII;
    },
    closeCookieConsent(){
      this.activeCookieConsent = !this.activeCookieConsent;
    },

    toggleCookiePolicy(){
      this.activeCookiePolicy = !this.activeCookiePolicy;
      console.log("toggleCookiePolicy() pressed.")
      console.log(this.activeCookiePolicy)
    },
    closeSmallCookie(){
      this.activeSmallCookie = !this.activeSmallCookie;
    },
    oneSmallCookie(){
      setTimeout(this.closeSmallCookie, 3500)
      this.toggleCookiePolicy()
      this.closeCookieConsent()
      this.isActive = !this.isActive;
      console.log("Small cookie window open")
    },

    updateData(){
      this.reloadCheck = true;
      this.renderDeleteKey++;
      console.log("Update data func fired.");
    }
  }
};
</script>

<style>
button:hover{
cursor: pointer;
}
::-webkit-scrollbar {
  width: 20px;
}
/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 5px grey; 
  border-radius: 10px;
}
/* Handle */
::-webkit-scrollbar-thumb {
background: rgb(172,164,176);
background: linear-gradient(0deg, rgba(172,164,176,1) 0%, rgba(197,197,207,1) 12%, rgba(165,180,186,1) 35%, rgba(242,241,218,1) 75%, rgba(255,255,255,1) 100%);
border: 2px solid slateblue;
border-radius: 10px;
}

/* Cookies */
.cookieConsent{
z-index: 10;
display: block;
position: fixed;
top: 0;
left: 0;
height: 100vh;
width: 100%;
background-image: url("assets/images/plateOfCookiesI.jpg");
background-repeat: no-repeat;
background-size: cover;
text-align: center;
}
.cookieConsent h1{
position: relative;
top: 400px;
height: 300px;
width: 100%;
font-size: 2rem;
font-family: hominFun;
background-color: rgba(255, 255, 255, 0.2);
}
.cookieConsent button{
z-index: 12;
position: relative;
top: 270px;
height: 8vh;
width: 40%;
font-family: hominFun;
font-size: 2rem;
}
.cookieConsentClosed{
  display: none;
}

.cookiePolicyViewLink{
color: blue; 
text-decoration: underline;
}
.cookiePolicyViewLink:hover{
cursor: pointer;
}
.cookiePolicyView{
z-index: 13;
display: block;
position: fixed;
top: 0;
left: 0;
height: 100vh;
width: 100%;
background: whitesmoke;
text-align: center;
overflow-x: hidden;
overflow-y: scroll;
}
.cookiePolicyView h1, h2, p{
font-family: hominFun;
}
.cookiePolicyView h1{
padding: 10px 10px 5px;
font-size: 5rem;
}
.cookiePolicyView h2{
padding: 15px 0px 15px;
font-size: 2.5rem;
}
.cookiePolicyView p{
padding: 0 10px 0;
font-size: 2rem;
}
.cookiePolicyView img{
border-radius: 0;
width: auto;
margin: 0 0 30px;
}
.cookiePolicyView button{
top: 0;
padding: 0 10px 0;
width: 100px;
border-radius:  15px;
margin-bottom: 30px;
}
.justOneSmallCookie{
display: none;
z-index: 12;
position: fixed;
top: 0;
left: 0;
height: 100vh;
width: 100vw;
text-align: center;
font-family: hominFun;
background: rgba(0, 0, 0, 0.75);
}
.smallCookieBox{
height: 80vh;
width: 80vw;
position: fixed;
top: 10vh;
left: 10vw;
background: rgb(255, 255, 255);
border: 2px solid #000;
border-radius: 50px 0;
}
.smallCookieBox h2{
position: relative;
top: 10px;
font-size: 2.5rem;
}
.smallCookieBox img{
border-radius: 0;
height: 80%;
width: 60%;
}
.active{
display: block;
}
/* Navbar and Button*/
.navbar{
position: fixed;
z-index: 1;
background-color:white;
text-align: center;
transition: 0.25s 0s ease-in-out;
}
.navbarClosed{
border-radius: 50% 50%;
}
.navbarOpen{
top: 0;
left: 0;
height: 100vh;
width: 100%;
border-radius: 0% 0%;
font-size: 3rem;
}
.navbar ul{
margin-top: 20px;
text-decoration: none;
}
.navbar li{
padding: 20px 0;
}
.navbar a{
text-decoration: none;
font-family: hominFun;
color: black;
}
.navbar button{
position: fixed;
margin-left: auto;
margin-right: auto;
border: 2px solid #000;
border-radius: 50% 50%;
background-color: white;
outline: none;
}
.slice{
position: relative;
margin-left: auto;
margin-right: auto;
height: 5px;
width: 35px;
background-color: #000;
transform-origin: center;
transition: 0.5s ease-in-out;
border-radius: 5px;
}
.sliceI{
top: -1.5px;
}

.sliceIII{
top: 2px;
}
.sliceITurn{
transform: rotate(135deg);
top: 3px;
left: 1px;
}
.sliceIITurn{
transform: rotate(45deg);
top: -2px;
left: 1px;
}
.sliceIIITurn{
transform: rotate(135deg);
display: none;
}
.listClosed{
display: none;
}
.listOpen{
display: block;
}
/* Shared Modal Styles */
.createAndUpdateModals{
position: relative;
top: 60px;
margin-right: auto;
margin-left: auto;
text-align: center;
background: rgba(255, 255, 255, 0.25);
border-radius: 100px 0px;
height: 85vh;
width: 84%;
font-family: hominFun;
}
.createAndUpdateModals h1{
position: relative;
top: 25vh;
padding: 0 20px;
font-size: 2rem;
}
.createAndUpdateModals button{
position: relative;
top: 35vh;
width: 25vw;
}
/* Shared Styles */
.container{
width: 100%;
height: 100vh;
margin: 0 auto;
overflow-x: hidden;
overflow-y: auto;
scroll-snap-type: y mandatory;
}
.snapAlign{
scroll-snap-align: start;
}

@font-face{
font-family: affair;
src: url("assets/fonts/affair/affair.otf") format("opentype");
}
@font-face{
font-family: hominFun;
src: url("assets/fonts/hominFun/hominFun.otf") format("opentype");
}
*{
padding: 0;
margin: 0;
}
html, body{
height: 100%;
width: 100%;
scroll-behavior: smooth;
}
.sectionBackgrounds{
background-size: cover;
background-repeat: no-repeat;
height: 100vh;
width: 100%;
}
/*** Small Phone and up ***/
/* Navbar and Button */
.navbar{
top: -15%;
right: -15%;
height: 70px;
width: 70px;
}
.navbar button{
top: 5%;
right: 2%;
height: 70px;
width: 70px;
}
.navbarOpen{
top: 0;
left: 0;
height: 100vh;
width: 100%;
}
/* Common Stles */
.centralBox{
position: relative;
top: 60px;
margin-right: auto;
margin-left: auto;
text-align: center;
background: rgba(255, 255, 255, 0.25);
border-radius: 100px 0px;
}
.centralBox h2{
position: relative;
top: 20px;
font-family: affair;
color: #fffdd0;
font-size: 2.5em;
letter-spacing: 4px;
}
.inputFields{
position: relative;
top: 40px;
height: 45px;
width: 70vw;
font-size: 1.5em;
background: rgba(255,255,255, 0.75);
border-radius: 30px 0px;
font-family: hominFun;
}
.centralBox button{
height: 40px;
width: 45vw;
font-size: 1.5em;
border: none;
font-family: hominFun;
}
.centralBox i{
color: #000;
}
option[value=""][disabled] {
display: none;
}
.inputTextField{
height: 200px;
}
.centralBox select{
height: 45px;
width: 70vw;
font-size: 1.5em;
font-family: hominFun;
}
.centralBox option{
font-size: 0.25em;	
}
/* XL Phone and up */
@media only screen and (min-device-width : 450px){
/* Cookies Consent */
.cookieConsent h1{
font-size: 1.8rem;
}
.cookieConsent button{
top: 53vh;
width: 30vw;
}
.cookieConsent h1{
top: 470px;
height: 230px;
}
/* Navbar */
.navbar button{
top: 4%;
right: 3%;
}
/* Modals */
.createAndUpdateModals{
height: 85vh;
width: 80%;
}
/* Common */
.centralBox{
height: 85vh;
width: 80%;
}
.centralBox h2{
top: -10px;
font-size: 3.5em;
}
.inputFields{
top: 0px;
height: 7vh;
width: 60vw;
font-size: 1.5em;
border-radius: 25px 0;
}
.centralBox select{
margin-top: -8vh;
height: 7vh;
width: 60vw;
font-size: 1.5em;
border-radius: 25px 0;
}
.centralBox option{
font-size: 1em;
}
.inputTextField{
height: 200px;
}
.centralBox button{
top: 190px;
height: 7vh;
width: 30vh;
font-size: 1.75em;
}
}
/* Tablet and up */
@media only screen and (min-device-width : 600px){
/* Cookies Consent */
.cookieConsent{
background-image: url("assets/images/plateOfCookiesII.jpg");
}
.cookieConsent h1{
top: 470px;
height: 230px;
}
.cookieConsent button{
width: 20vw;
}
/* Navbar and Button */
.navbar{
top: -20%;
right: -20%;
}
.navbar button{
top: 2%;
right: 4%;
height: 90px;
width: 90px;
}
.navbarOpen{
top: 0;
left: 0;
height: 100vh;
width: 100%;
}
.slice{
height: 7px;
width: 50px;
}
.sliceI{
top: -3px;
}
.sliceIII{
top: 3px;
}

.sliceIITurn{
top: -3px;
}
.centralBox{
width: 80%;
border-radius: 100px 0;
}
.centralBox h2{
font-size: 4.5em;
}
.inputFields{
top: -20px;
height: 6vh;
width: 60vw;
font-size: 2em;
border-radius: 15px 0;
}
.centralBox select{
width: 60vw;
font-size: 2em;
}
.centralBox option{
font-size: 0.75em;
}
.inputTextField{
height: 200px;
}
.centralBox button{
top: 60px;
height: 7vh;
width: 35vh;
font-size: 2em;
}
}
/* M Tablet and up */
@media only screen and (min-device-width : 750px){
/* Cookies Consent */
.cookieConsent h1{
padding-top: 20px;
}
.cookieConsent button{
top: 51vh;
width: 20vw;
}
.smallCookieBox img{
width: 45%; 
}
/* Modals */
.createAndUpdateModals{
width: 70%;
}
/* Navbar and Button */
.navbar button{
top: 2%;
right: 9.5%;
}
.centralBox{
width: 70%;
}
.centralBox h2{
top: 10px;
font-size: 4em;
}
.inputFields{
top: 25px;
width: 60vw;
font-size: 2em;
border-radius: 15px 0;
}
.centralBox select{
width: 60vw;
border-radius: 10px 0;
font-size: 2em;
}
.inputTextField{
height: 180px;
}
.centralBox button{
top: 200px;
height: 6vh;
width: 30vh;
font-size: 2em;
}
}
/* L Tablet and up */
@media only screen and (min-device-width : 1000px){
/* Cookies Consent */
.cookieConsent{
background-image: url("assets/images/plateOfCookiesIII.jpg");
}
.cookieConsent h1{
top: 75vh;
padding: 30px 0;
height: 200px;
background-color: rgba(255, 255, 255, 0.5);
}
.cookieConsent button{
top: 54vh;
width: 10vw;
}
.smallCookieBox{
width: 45vw;
left: 27%;
}
.smallCookieBox img{
width: 60%;
}
/* Navbar and Button */
.navbar button{
top: 2%;
right: 4%;
}
.navbarOpen{
top: 0;
left: 0;
height: 100vh;
width: 100%;
}
.centralsBox select{
border-radius: 15px 0;
}
.inputFields{
top: 0;
width: 55vw;
}
.inputTextField{
height: 150px;
}
.centralBox button{
top: 200px;
}
}
/* Laptop and up */
@media only screen and (min-device-width : 1300px){
.smallCookieBox img{
width: 50%; 
}
.navbar button{
right: 2%;
}
.createAndUpdateModals{
width: 50%;
}
.createAndUpdateModals h1{
font-size: 2.5rem;
}
.centralBox{
  width: 50%;
}
.centralBox h2{
font-size: 5em;
width: 60%;
}
.inputFields{
width: 40vw;
top: -35px;
}
.centralBox select{
width: 40vw;
}
.centralBox button{
top: 200px;
height: 6vh;
width: 30vh;
font-size: 2em;
}
}
</style>
