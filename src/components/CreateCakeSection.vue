<template>
  <section id="createCakeSection" class="sectionBackgrounds">
    <!-- Modal Views -->
    <div v-if="confirmCreate" class="createAndUpdateModals">
      <h1>New cake created.</h1>
      <button @click="confirmCreateModalFunc(), reloadEvent()">OK</button>
    </div>

    <div v-if="displayCreateValidateYum" class="createAndUpdateModals">
      <div class="validationModal">
        <h1>Please choose a Yum Factor between 1 and 5.</h1>
        <button @click="confirmCreateModalFunc()">OK</button>
      </div>
    </div>

    <!-- Main View -->

    <div class="createCakeBox centralBox" v-if="displayCreateBox">
      <h2>New Cake</h2>
      <form id="createForm" @submit.prevent>
        <input
          type="text"
          name="createName"
          id="createName"
          class="inputFields"
          placeholder="Cake Name..."
          v-model="createCakeName"
        />
        <input
          type="number"
          name="createYum"
          id="createYum"
          class="inputFields"
          min="1"
          max="5"
          placeholder="Yum Factor..."
          v-model="createCakeYumFactor"
        />
        <input
          type="text"
          name="createImg"
          id="createImg"
          class="inputFields"
          placeholder="Image URL..."
          v-model="createCakeUrl"
        />
        <textarea
          name="createReview"
          id="createReview"
          class="inputFields inputTextField"
          placeholder="Review..."
          rows="5"
          cols="60"
          v-model="createCakeReview"
        ></textarea>
        <button
          type="button"
          id="createButton"
          :disabled="!createFormValid"
          @click="
          confirmCreateModalFunc(),
          sendPostRequest()"
          >Create 
          <i class="fa fa-plus"></i>
        </button>
      </form>
    </div>
  </section>
</template>

<script>
import axios from "axios";
export default {
props: [
"reload"
],
emits: [
"update"
],
  data() {
    return {
      confirmCreate: false,
      displayCreateValidateYum: false,
      displayCreateBox: true,

      createCakeName: "",
      createCakeYumFactor: "",
      createCakeUrl: "",
      createCakeReview: "",
    };
  },
  methods: {
 sendPostRequest() {
 axios({
  method: 'post',
  url: 'https://samuel-davidson.co.uk/mmmDelicous/backend/rBja6258CxqhFHxT/createSSEP.php',
  data: {
    name: this.createCakeName,
    yumFactor: this.createCakeYumFactor,
    imageUrl: this.createCakeUrl,
    comment: this.createCakeReview,
  },
  headers : {

    "Access-Control-Allow-Headers": "Content-Type",
    "Access-Control-Allow-Origin": "*",
    "Access-Control-Allow-Methods": "*",
  },
})
.then((response) => {
          console.log(response);
        });
    },

    createHasData: function(value) {
      if (value.length > 0) {
        return true;
      } else {
        return false;
      }
    },
    confirmCreateModalFunc: function() {
      this.displayCreateBox = !this.displayCreateBox;
      if (
        this.createCakeYumFactor == "1" ||
        this.createCakeYumFactor == "2" ||
        this.createCakeYumFactor == "3" ||
        this.createCakeYumFactor == "4" ||
        this.createCakeYumFactor == "5"
      ) {
        this.confirmCreate = !this.confirmCreate;
      } else {
        this.displayCreateValidateYum = !this.displayCreateValidateYum;
      }
    },
    reloadEvent(){
      this.$emit("update", true)
    }
  },
  computed: {
    createFormValid: function() {
      if (
        this.createHasData(this.createCakeName) &&
        this.createHasData(this.createCakeYumFactor) &&
        this.createHasData(this.createCakeUrl) &&
        this.createHasData(this.createCakeReview)
      ) {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
}
#createCakeSection {
  background-image: url("../assets/images/baking.jpg");
  border-top: 0.5px solid #fffdd0;
}

/* Create section box */
.createCakeBox {
  height: 85vh;
  width: 84%;
}
#createForm {
  z-index: 0;
  position: relative;
  top: -30px;
}
.createCakeBox button {
  position: relative;
  top: 70px;
}
/* XL Phone and up */
@media only screen and (min-device-width: 450px) {
  #createForm {
    top: -35px;
  }
  .inputTextField {
    height: 250px;
  }
  #createButton {
    position: relative;
    top: 20px;
  }
}
/* Tablet and up */
@media only screen and (min-device-width: 600px) {
  #createForm {
    top: -30px;
  }
  #createButton {
    top: -10px;
    height: 7vh;
    width: 35vh;
    font-size: 2.5em;
  }
}
/* M Tablet and up */
@media only screen and (min-device-width: 750px) {
  #createCakeSection {
    background-image: url("../assets/images/bakingII.jpg");
  }
  .centralBox {
    width: 50%;
  }
  .createCakeBox h2 {
    font-size: 4em;
  }
  #createForm {
    top: -45px;
  }
  .inputTextField {
    height: 180px;
  }
  #createButton {
    top: 35px;
  }
  .createCakeBox i {
    color: #000;
  }
}
/* Laptop and up */
@media only screen and (min-device-width: 1000px) {
  #createForm {
    top: -15px;
  }
  #createButton {
    top: 25px;
  }
}

/* Laptop and up */
@media only screen and (min-device-width: 1300px) {
  #createCakeSection {
    background-image: url("../assets/images/bakingIV.jpg");
  }
  #createForm {
    top: 10px;
  }
  #createButton {
    top: -25px;
  }
}
</style>
