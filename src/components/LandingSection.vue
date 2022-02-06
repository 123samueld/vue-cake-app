<template>
<section id="landingSection" class="sectionBackgrounds">
<h1 class="smallH1">Mmm...</h1>
<h1 class="largeH1">Mmm... Delicious!</h1>
<h2 class="smallH2">Love Cake?</h2>
<h2 class="largeH2">You've come to the right place!</h2>
</section>
</template>

<script>
export default {
name: 'LandingSection',
}
</script>

<style>
/* All Devices */
*{
padding: 0;
margin: 0;
}
.smallH1, .largeH1, .smallH2, .largeH2{
position: relative;
width: fit-content;
margin-left: auto;
margin-right: auto;
text-align: center;
color: #fffdd0;
}
.centralBox h2 {
margin-left: auto;
margin-right: auto;
}
.smallH1, .largeH1{
position: relative;
font-family: affair;
letter-spacing: 4px;
}
.smallH2, .largeH2{
font-family: hominFun;
}
/* Phone First Style */
#landingSection{
background-image: url("../assets/images/sliceOfCakeIII.jpg");
}
.smallH1, .smallH2{
font-size: 4rem;
}
.smallH2{
top: 200px;
}
.largeH1{
display: none;
}
.largeH2{
display: none;
}
/* XL Phone and up */
@media only screen and (min-device-width : 450px){
#landingSection{
background-image: url("../assets/images/sliceOfCakeII.jpg");
}
}

/* S Tablet and up */
@media only screen and (min-device-width : 600px){
#landingSection{
background-image: url("../assets/images/sliceOfCake.jpg");
}
.smallH2{
top: 250px;
}
}
/* M Tablet and up */
@media only screen and (min-device-width : 750px){
#landingSection{
background-image: url("../assets/images/largeWelcomeCake.jpg");
}
.smallH1{
display: none;
}
.largeH1, .largeH2{
display: block;
}
.largeH1{
height: 150px;
width: 100%;
font-size: 4rem;
background-color: rgba(0, 0, 0, 0.2);
letter-spacing: 5px;
}
.smallH2, .largeH2{
top: 120px;
background-color: rgba(0, 0, 0, 0.2);
font-size: 2.5rem;
border-radius: 15px 0;
}
}

/* L Tablet and up */
@media only screen and (min-device-width : 1000px){
.largeH1{
font-size: 5rem;
}
.smallH2, .largeH2{
font-size: 2.5rem;
}
}
/* Small Laptop and Up */
@media only screen and (min-device-width : 1200px){
.largeH1{
font-size: 6rem;
letter-spacing: 6px;
}
}
/* Laptop and up */
@media only screen and (min-device-width : 1450px){
.largeH1{
height: 180px;
font-size: 6rem;
}
.smallH2, .largeH2{
top: 160px;
font-size: 3.5rem;
}
}

</style>