<template>
  <div id="app">      
      <div class="wrapper">
        <app-header :user-name="this.user.name" />    
        <products-list :products="products"/>
      </div>
  </div>
</template>



<script>
import { EventBus } from './event-bus.js';
import ProductsList from './components/ProductsList';
import AppHeader from './components/AppHeader';

export default {
  name: 'app',  
  data () {    
    return {
      token:'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI1YTExOWFlMzczODUzNDAwNjg0NDUxNzIiLCJpYXQiOjE1MTExMDMyMDN9.KO6JO0Nir3MhRdMOA-lfHhO1cBpg_4VAL0pi6j6Lgqc',
      user:[],
      products:[]      
    }
  },

  // COMPONENTS
  // -------------
  components: {
    ProductsList, 
    AppHeader
  },


  // METHODS
  // -------------
  methods: {
    
    // Petition get to receive the list of products
    loadProducts() {  
      this.$http.get(`https://aerolab-challenge.now.sh/products?token=${this.token}`)
        .then((response) => {
          this.products= response.data;
        })
        .catch((error) => {
          console.log(error)  
        })
    },    


    autoLogin() {
      this.$http.get(`https://aerolab-challenge.now.sh/user/me?token=${this.token}`)
        .then((response) => {
          this.user= response.data;          
          EventBus.$emit('user-points', this.user.points); // envio los puntos del usuario al bus                    
        })
    }
  },


  // CREATED
  // -------------
  created() {
    this.autoLogin();
    this.loadProducts();
  },


}
</script>


<style lang="postcss"  src="./assets/css/app.css" />



