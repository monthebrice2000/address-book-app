<template>
  <div class="button" @click="open">
    <svg class="logo" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M432 256c0 17.69-14.33 32.01-32 32.01H256v144c0 17.69-14.33 31.99-32 31.99s-32-14.3-32-31.99v-144H48c-17.67 0-32-14.32-32-32.01s14.33-31.99 32-31.99H192v-144c0-17.69 14.33-32.01 32-32.01s32 14.32 32 32.01v144h144C417.7 224 432 238.3 432 256z"/></svg>
    <span class="title">Add Address</span>
  </div>
  <form @submit.prevent="sendData" class="form">
    <div class="container">
      <div class="item">
        <span class="title">Add Address</span>
        <svg @click="closeR" class="logo" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--! Font Awesome Pro 6.0.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M432 256c0 17.69-14.33 32.01-32 32.01H256v144c0 17.69-14.33 31.99-32 31.99s-32-14.3-32-31.99v-144H48c-17.67 0-32-14.32-32-32.01s14.33-31.99 32-31.99H192v-144c0-17.69 14.33-32.01 32-32.01s32 14.32 32 32.01v144h144C417.7 224 432 238.3 432 256z"/></svg>
      </div>
      <div class="item">
        <h3 class="label">How should your email be addressed? </h3>
        <input type="text" placeholder="E.g The Smith Family" name="family" ref="family" v-model="family" required>
      </div>
      <div class="item">
        <h3 class="label">First Name</h3>
        <h3 class="label">Last Name </h3>
        <input type="text" placeholder="The First Name" name="first_name" ref="first_name" v-model="first_name" required>
        <input type="text" placeholder="The Last Name" name="last_name" ref="last_name" v-model="last_name" required>
      </div>
      <div class="item">
        <h3 class="label">Email</h3>
        <h3 class="label">Phone</h3>
        <input type="email" placeholder="The Email" name="email" ref="email" v-model="email" required>
        <input type="text" placeholder="The Phone Number" name="phone" ref="phone" v-model="phone" required>
      </div>
      <div class="item">
        <h3 class="label">Street Address</h3>
        <h3 class="label">Postal Code</h3>
        <input type="text" placeholder="Street address, apartment, no" name="street_address" ref="street_address" v-model="street_address" required>
        <input type="number" placeholder="60323" name="postal_code" ref="postal_code" v-model="postal_code" required>
      </div>
      <div class="item">
        <h3 class="label">City</h3>
        <h3 class="label">Country</h3>
        <input type="text" placeholder="The City Name" name="city" ref="city" v-model="city" required>
        <div class="countries">
          <input type="text" placeholder="--- Country ---" name="country" ref="country" v-model="country" required disabled>
          <div class="all_countries" @click="selectCountry">
            <span class="country">CAMEROON</span>
            <span class="country">NIGERIA</span>
            <span class="country">CONGO</span>
            <span class="country">RWANDA</span>
            <span class="country">SUD AFRICA</span>
            <span class="country">ETHIOPIA</span>
            <span class="country">GUINNEE</span>
            <span class="country">GHANA</span>
          </div>
        </div>
      </div>
      <div class="item">
        <h3 class="label">Labels</h3>
        <div class="labels">
          <input type="text" placeholder="--- Labels ---" name="labels" ref="labels" v-model="labels" required disabled>
          <div class="all_labels" @click="selectLabel">
            <span class="label">Friends</span>
            <span class="label">Collegues</span>
            <span class="label">Family</span>
          </div>
        </div>
      </div>
      <input class="item" type="submit" name="submit" value="Save">
    </div>
  </form>
</template>

<script>
  /* eslint-disable */
  import $ from 'jquery';


export default {
  name: 'AddButton',
  props : ['ad'],
  emits: ['addNewAddress'],
  beforeMount() {
    console.log( "mounted" , this.ad )
  },
  beforeUpdate() {
    console.log( this.buttonActive )
    if( this.buttonActive ){
      return;
    }
    if( this.ad !== null && this.ad ){
      this.buttonActive = true;
      this.family = this.ad.family;
      this.phone = this.ad.phone;
      this.country = this.ad.location;
      this.city = this.ad.place;
      this.postal_code = this.ad.postal_code;
      this.email = this.ad.email;
      this.first_name = this.ad.propert.split(' ')[0];
      this.last_name = this.ad.propert.split(' ')[1];
      this.street_address = this.ad.street_address;
      this.labels = this.ad.labels;
      this.labels = this.labels[0];
    }

  },
  data : function(){
    return {
      family : null,
      first_name : null,
      last_name : null,
      email : null,
      phone : null,
      street_address : null,
      labels : null,
      city: null,
      country : null,
      postal_code : null,
       buttonActive : false,
    }
  },
  computed : {
  },
  methods : {
    sendData(){
      const newAddress = {
        location : this.country,
        place : this.city,
        phone : this.phone,
        propert : this.first_name + ' ' + this.last_name,
        labels : [ this.labels ],
        family : this.family,
        street_address : this.street_address,
        postal_code : this.postal_code,
        email : this.email,
      }
      this.last_name = '';
      this.first_name = '';

      this.$emit( 'addNewAddress', newAddress );

      $(".form").toggleClass("active");
      this.buttonActive = false;

    },
    selectCountry(e){
      this.country = e.target.textContent;
    },
    selectLabel(e){
      this.labels = e.target.textContent;
    },
    open(){
      this.buttonActive = true;
      this.family = '';
      this.phone = '';
      this.country = '';
      this.city = '';
      this.postal_code = '';
      this.email = '';
      this.first_name = '';
      this.last_name = '';
      this.street_address = '';
      this.labels = '';
      $(".form").toggleClass("active");
      // console.log( this.buttonActive )
    },
    closeR(){
      this.buttonActive = false;
      $(".form").toggleClass("active");
      // console.log( this.buttonActive )
    }
  },
  mounted() {
    $(".countries").click( function() {
      $(".countries .all_countries").toggleClass("active");
    })
    $(".labels").click( function() {
      $(".labels .all_labels").toggleClass("active");
    })
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
