<template>
    <div>
      <popup-confirm :class="{show:showPopup, hide:!showPopup}" >Redeem {{productPopup}} for <strong>{{costPopup}} points</strong>.</popup-confirm>
        
        <div class="container blur">

          <div class="filters-wrap">
            <div>
              <transition name="detail-listFx">
                <span class="detail-list" v-if="$refs.paginator"> {{$refs.paginator.pageItemsCount}} results</span> 
              </transition>

              <div class="sort-wrap">
                <span class="sort-title">Sort by:</span>                
                <a class="btn sort" :class="{ active: btnRecentActive }"  @click="productFilter='lowestSort'">Most recent</a>
                <a class="btn sort" :class="{ active: btnLowestActive }"  @click="sortProductList('lowest')">Lowest price</a>
                <a class="btn sort" :class="{ active: btnHighestActive }" @click="sortProductList('highest')">Highest price</a>
              </div>           

            </div>            
            <paginate-links for="products" :async="true" @change="pageLinkChange" :simple="{next: ' ',prev: ' '}"></paginate-links>
          </div>
          
          <div class="products-list">  
            <paginate class="paginate-list" name="products" :per="16"  :list="products" ref="paginator" v-if="true">              
                  <product v-for="(product,key) in paginated('products')" :key="product._id"                                        
                    :id="product._id"          
                    :name="product.name"
                    :cost="product.cost"
                    :missingPoints="getMissingPoint(product.cost)"
                    :category="product.category"
                    :imgUrl="product.img.url"
                    :imgHdUrl="product.img.hdUrl">          
                  </product>
              
            </paginate>  

            <div class="filters-wrap footer">
              <div>
                <span class="detail-list" v-if="$refs.paginator"> {{$refs.paginator.pageItemsCount}} results</span>            
              </div>            
              <paginate-links for="products" :async="true" @change="pageLinkChange" :simple="{next: ' ',prev: ' '}"></paginate-links>            
            </div>
          </div> 
        </div>   
    </div>
</template>


<script>

import Product from './Product';
import PopupConfirm from './PopupConfirm';
import { EventBus } from '../event-bus.js';


export default {
  name:'products-list',

  data () {
    return {
      productsDefault: Array,
      productFilter:'recent',
      userPoints:'',   
      selectedOrder:'recent',
      // items: ['Item One', 'Item Two', 'Item Three', 'Item Four', 'Item Five', 'Item Six', 'Item Seven', 'Item Eight', 'Item Nine', 'Item Ten', 'Item Eleven', 'Item Twelve', 'Item Thirteen'],
      paginate: ['products'],
      showPopup:false,
      btnRecentActive: false,
      btnLowestActive: false,
      btnHighestActive: false,
      productPopup:'',
      costPopup:0
      // minimum:2000
    }
  },

  // COMPONENTS
  // -------------
  components:{
    Product,
    PopupConfirm
  },


  // PROPERTIES
  // -------------
  props: {
    products: Array    
  },


  // METHODS
  // -------------
  methods: {

    pageLinkChange (toPage, fromPage) {
      console.log(toPage);
      },

    sortProductList(order) {    
      switch(order) {
        case 'recent':
          this.products = this.productsDefault;  // FALTA TERMINAR ESTE
          this.btnRecentActive = true;
          this.btnLowestActive = false;
          this.btnHighestActive = false;              
          break;

        case 'lowest':
          this.products = this.products.sort( (a, b) =>  a.cost - b.cost);
          this.btnRecentActive = false;
          this.btnLowestActive = true;
          this.btnHighestActive = false;
          break;

        case 'highest':
          this.products = this.products.sort( (a, b) =>  b.cost - a.cost);
          this.btnRecentActive = false;
          this.btnHighestActive = true;
          this.btnLowestActive = false;
          break;
      }
    },

    getMissingPoint(cost) {      
      //cost > this.userPoints ? (cost - this.userPoints) : false      
      if(cost > this.userPoints)
        return (cost - this.userPoints)
      else
        return false
    }
   
  },


  computed : {
    defaultSort() {
      return this.productList;
    },

    lowestSort() {
      return this.products.sort( (a, b) =>  a.cost - b.cost);
    },

    highest() {
      return this.products.sort( (a, b) =>  b.cost - a.cost);
    }    

  },


  created () {
    EventBus.$on('user-points', (points) => this.userPoints = points);        
    EventBus.$on('show-popup', (points, product) => {
      
      //Add class bodyOff to body
      document.querySelector('body').classList.add('bodyOff')            
      this.productPopup = product;
      this.costPopup = points;
      this.showPopup= true;
    }),

    EventBus.$on('close-popup', () => {
      this.showPopup= false;
      document.querySelector('body').classList.remove('bodyOff')
    });

    EventBus.$on('discountPoints', (cost)=> {
      EventBus.$emit('user-points',this.userPoints-=cost);
    });

    EventBus.$on('discount-Points', ()=> {
      EventBus.$emit('user-points',this.userPoints-= this.costPopup);          
    });           
  },
}
</script>


<style lang="postcss" scoped>

  .container {
    padding-top: 47px;
  }

  .filters-wrap {
    display: flex;    
    justify-content: space-between;
    align-items: center;    
    font-size:24px;
    padding: 20px 0;
    margin-bottom: 42px;
    border-bottom: 1px solid #D9D9D9;

    .sort-wrap {
      display: inline-flex;
    }

    .sort-title {
      white-space: nowrap;
      margin-right: 18px;
    }

    .detail-list {
      padding:10px 24px 10px 0;
      margin-right: 24px;
      border-right: 1px solid #D9D9D9;
      color: #616161;
      //color: var(--text-silver-dark);    
    }   

    span {
      align-self:center;     
      color: #A3A3A3;
      //color: var(--text-silver-clear);
    }

    .btn.sort {
        margin: 0 12px;
        transition: all .5s;
        opacity: 1;
        
        &.active {
          pointer-events: none;             
        }        

        &:hover:not(.active) {
          opacity: .8;
        }        
    }

    .paginate-links {
      display: flex;
    }
  }

  .paginate-list {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr 1fr;
    grid-column-gap: 24px;
    grid-row-gap: 24px;
  }

  .footer {      
    .detail-list{
      border-right:none;
    }
  } 

  /*** Medias query ***/
  @media (max-width: 1100px) {
    .paginate-list {		
      grid-template-columns: 1fr 1fr 1fr;        
    }

    .filters-wrap {
      display: block;
      text-align: center;
      flex-wrap: wrap;

      .detail-list {
        border-right: 0;
        margin-right: 0;
        margin-bottom: 10px;
        padding:10px 0;          
      }

      .sort-wrap {
        display: block;
        
        .sort {
          margin: 10px;
        }
      }
    }

    .paginate-links {
      justify-content: center;
      margin: 22px 0;
    }      
  }

  @media (max-width: 760px) {
    .paginate-list {		
      grid-template-columns: 1fr 1fr;
    }
    .filters-wrap {
      .sort-title {
        display: none;
      }
    }
  }

@media (max-width: 480px) {
    .paginate-list {		
      grid-template-columns: 1fr;
    }
  }    

</style>






