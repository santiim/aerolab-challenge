<template>    
    <transition name="itemfX" appear>
        <li class="product" v-on:mouseenter="show" v-on:mouseleave="hide" :class="{productOver: showHover}">    

            <!-- If you do not have enough points, I show the necessary ones, otherwise it shows purchase icon -->
            <div class="missing-points" v-if="missingPoints"><span>you need {{missingPoints}} </span>
                <i>
                    <svg viewBox="0 0 34 34" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><defs><filter x="-9.1%" y="-9.1%" width="128.3%" height="128.3%" filterUnits="objectBoundingBox" id="filter-1"><feOffset dx="2" dy="2" in="SourceAlpha" result="shadowOffsetOuter1"></feOffset><feGaussianBlur stdDeviation="2" in="shadowOffsetOuter1" result="shadowBlurOuter1"></feGaussianBlur><feColorMatrix values="0 0 0 0 0   0 0 0 0 0   0 0 0 0 0  0 0 0 0.1 0" type="matrix" in="shadowBlurOuter1" result="shadowMatrixOuter1"></feColorMatrix><feMerge><feMergeNode in="shadowMatrixOuter1"></feMergeNode><feMergeNode in="SourceGraphic"></feMergeNode></feMerge></filter><radialGradient cx="50%" cy="50%" fx="50%" fy="50%" r="68.6284858%" id="radialGradient-2"><stop stop-color="#FFCF00" offset="0%"></stop><stop stop-color="#F7AE15" offset="100%"></stop></radialGradient></defs><g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd"><g id="Catalog-pg1" transform="translate(-609.000000, -731.000000)"><g id="products" transform="translate(132.000000, 622.000000)"><g id="line-1"><g id="product-card-hover" filter="url(#filter-1)" transform="translate(300.000000, 0.000000)"><g id="money" transform="translate(71.000000, 100.000000)"><g transform="translate(108.000000, 11.000000)"><g><circle id="Oval-Copy-3" fill="url(#radialGradient-2)" cx="13" cy="13" r="13"></circle><path d="M13,3.0952381 C7.54580357,3.0952381 3.0952381,7.54657738 3.0952381,13 C3.0952381,18.4541964 7.54657738,22.9047619 13,22.9047619 C18.4541964,22.9047619 22.9047619,18.4534226 22.9047619,13 C22.9047619,7.54580357 18.4534226,3.0952381 13,3.0952381 Z M13,21.7440476 C8.17850893,21.7440476 4.25595238,17.8214911 4.25595238,13 C4.25595238,8.17850893 8.17850893,4.25595238 13,4.25595238 C17.8214911,4.25595238 21.7440476,8.17850893 21.7440476,13 C21.7440476,17.8214911 17.8214911,21.7440476 13,21.7440476 Z" id="Shape" fill="#F8B013" fill-rule="nonzero"></path><path d="M13,5.2962963 C8.76834769,5.2962963 5.2962963,8.76956614 5.2962963,13 C5.2962963,17.2316523 8.76956614,20.7037037 13,20.7037037 C17.2316523,20.7037037 20.7037037,17.2304339 20.7037037,13 C20.7037037,8.76834769 17.2304339,5.2962963 13,5.2962963 Z M13,19.5245654 C9.40233107,19.5245654 6.47543462,16.5976689 6.47543462,13 C6.47543462,9.40233107 9.40233107,6.47543462 13,6.47543462 C16.5976689,6.47543462 19.5245654,9.40233107 19.5245654,13 C19.5245654,16.5976689 16.5976689,19.5245654 13,19.5245654 Z" id="Shape" fill="#F8B013" fill-rule="nonzero"></path></g></g></g></g></g></g></g></g></svg>
                </i>
            </div>    

            <div class="buy-icon" v-else>
                <svg width="42" height="42" viewBox="0 0 42 42" xmlns="http://www.w3.org/2000/svg"><defs><radialGradient cy="50.876%" fx="50%" fy="50.876%" r="79.847%" id="a"><stop stop-color="#0AD4FA" offset="0%"/><stop stop-color="#25BBF1" offset="100%"/></radialGradient></defs><g transform="translate(0 0)" fill="none">
                    <circle fill="" cx="21" cy="21" r="21"/><path class="bag" d="M29.995 29.108l-1.112-13.577c-.024-.305-.288-.541-.605-.541h-3.032v-1.06c0-1.615-1.36-2.93-3.032-2.93h-2.426c-1.672 0-3.032 1.314-3.032 2.93v1.06h-3.032c-.317 0-.581.236-.605.541l-1.112 13.577c-.039.487.136.971.479 1.329.343.358.83.563 1.335.563h14.361c.505 0 .992-.205 1.335-.563.343-.358.518-.843.479-1.329zm-11.995-14.858c0-1.241.807-2.25 1.8-2.25h2.4c.993 0 1.8 1.009 1.8 2.25v.75h-6v-.75z" fill-rule="nonzero"/></g></svg>
            </div>        
            

            <!-- Image according to screen type -->
            <div class="img-wrap">            
                <img :src="imgUrl" :srcset="`${imgUrl} 1x, ${imgHdUrl} 2x`">            
            </div>   

            
            <div class="data-wrap">
                <p class="category">{{ category }}</p>
                <h4> {{ name }} </h4>
            </div>  


            <!-- Content to show when positioning the mouse on the product -->
            <div class="hover" :class="{show: showHover}" v-if="!missingPoints">            
                <div>
                    <div class="cost-wrap">
                        <span>{{ cost }}</span>
                        <i>
                            <svg version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><defs><filter x="-9.1%" y="-9.1%" width="128.3%" height="128.3%" filterUnits="objectBoundingBox" id="filter-1"><feOffset dx="2" dy="2" in="SourceAlpha" result="shadowOffsetOuter1"></feOffset><feGaussianBlur stdDeviation="2" in="shadowOffsetOuter1" result="shadowBlurOuter1"></feGaussianBlur><feColorMatrix values="0 0 0 0 0   0 0 0 0 0   0 0 0 0 0  0 0 0 0.1 0" type="matrix" in="shadowBlurOuter1" result="shadowMatrixOuter1"></feColorMatrix><feMerge><feMergeNode in="shadowMatrixOuter1"></feMergeNode><feMergeNode in="SourceGraphic"></feMergeNode></feMerge></filter><radialGradient cx="50%" cy="50%" fx="50%" fy="50%" r="68.6284858%" id="radialGradient-2"><stop stop-color="#FFCF00" offset="0%"></stop><stop stop-color="#F7AE15" offset="100%"></stop></radialGradient></defs><g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd"><g id="Catalog-pg1" transform="translate(-609.000000, -731.000000)"><g id="products" transform="translate(132.000000, 622.000000)"><g id="line-1"><g id="product-card-hover" filter="url(#filter-1)" transform="translate(300.000000, 0.000000)"><g id="money" transform="translate(71.000000, 100.000000)"><g transform="translate(108.000000, 11.000000)"><g><circle id="Oval-Copy-3" fill="url(#radialGradient-2)" cx="13" cy="13" r="13"></circle><path d="M13,3.0952381 C7.54580357,3.0952381 3.0952381,7.54657738 3.0952381,13 C3.0952381,18.4541964 7.54657738,22.9047619 13,22.9047619 C18.4541964,22.9047619 22.9047619,18.4534226 22.9047619,13 C22.9047619,7.54580357 18.4534226,3.0952381 13,3.0952381 Z M13,21.7440476 C8.17850893,21.7440476 4.25595238,17.8214911 4.25595238,13 C4.25595238,8.17850893 8.17850893,4.25595238 13,4.25595238 C17.8214911,4.25595238 21.7440476,8.17850893 21.7440476,13 C21.7440476,17.8214911 17.8214911,21.7440476 13,21.7440476 Z" id="Shape" fill="#F8B013" fill-rule="nonzero"></path><path d="M13,5.2962963 C8.76834769,5.2962963 5.2962963,8.76956614 5.2962963,13 C5.2962963,17.2316523 8.76956614,20.7037037 13,20.7037037 C17.2316523,20.7037037 20.7037037,17.2304339 20.7037037,13 C20.7037037,8.76834769 17.2304339,5.2962963 13,5.2962963 Z M13,19.5245654 C9.40233107,19.5245654 6.47543462,16.5976689 6.47543462,13 C6.47543462,9.40233107 9.40233107,6.47543462 13,6.47543462 C16.5976689,6.47543462 19.5245654,9.40233107 19.5245654,13 C19.5245654,16.5976689 16.5976689,19.5245654 13,19.5245654 Z" id="Shape" fill="#F8B013" fill-rule="nonzero"></path></g></g></g></g></g></g></g></g></svg>
                        </i>
                    </div>
                    <a  class="btn redeem" v-if="!missingPoints" @click="reedemNow(cost, name)">Reedem now</a>
                </div>
            </div>   

        </li>       
    </transition> 
</template>


<script>

import { EventBus } from '../event-bus.js';

export default {
  name:'product',
  
data() {
    return {
        showHover: false,
    }
},
    // PROPERTIES
    // -------------
    props:{
        index: Number,     
        id: String,
        name: String,      
        cost: Number,
        category: String,
        imgUrl: String,
        imgHdUrl: String,
        missingPoints: [Number, Boolean]
    },
  

    // METHODS
    // -------------
    methods:{
        // It is responsible for processing the exchange of the product
        reedemNow(cost, productName) {
            EventBus.$emit('show-popup', cost, productName)
        },
        
        show() {            
             this.showHover = !this.showHover;
        },

        hide() {            
             this.showHover = !this.showHover;
        }        
    },    
}
</script>



<style lang="postcss" scoped>



.img-wrap {
    text-align: center;
    width: 95%;
    margin: 0 auto;           
    min-height: 12.1rem;
    transition: all 1s;

    img {
        width:100%;
    }
}


    
    
.product {           
    position: relative;  
    overflow: hidden;               
    box-shadow:2px 2px 4px 0 rgba(0,0,0,0.10); 
    background: #fff;
    padding: 12px 0 24px 0;
    transition:all 2s, box-shadow 2.3s ease-in-out;        
    box-sizing: border-box;

    &::after {
        content: '';
        position: absolute;
        background: #f9f9f9;
        position: absolute;
        z-index: 4;
        left: 0;
        top: 0;
        width: 100%;
        height: 100%;
        transform: translate(100%, 0);
        transition: all .9s cubic-bezier(0,1.01,.74,.98);  
    }

    .buy-icon {
        position: absolute;
        right: 12px;
        top: 12px;
        z-index: 3;
        svg > g > circle {
            fill:#43c9f5;            
        } 
        
        svg .bag {
            fill:#fff;
            transition: fill .5s ease-in-out;
        }
    }

    .hover {             
        position: absolute;
        text-align: center;
        overflow: hidden;
        transition: all 1s;           	
        transition-timing-function: cubic-bezier(0.2,1,0.3,1);                        
        border-radius:50%;
        width: 42px;
        height: 42px;
        top: 12px;
        right: 12px;
        z-index: 2;
        background:linear-gradient(-180deg, rgba(10,212,250,.9) 0%, rgba(37,187,241,.9) 100%);

        & > div {
            opacity: 0;
            position: relative;
            top: 56%;
            left: 50%;
            transform: translate(-50%, -50%);
            transition: transform 1s, opacity 2.6s;
            transition-timing-function: cubic-bezier(0.2,1,0.3,1);
            
            a {
                display: inline-block;
            }

            .cost-wrap {
                display: flex;
                justify-content: center;
                align-items: center;
                margin-bottom: 12px;

                span {
                    align-self: auto;
                    font-size:36px;
                    color:#fff;
                    margin-right:8px;
                }

                i {
                    width: 29px;
                    height: 29px;
                    display: block;
                    white-space: nowrap;
                    position: relative;
                    overflow: hidden;                

                    svg {
                        width: 100%;
                        position: absolute;
                        height: 100%;
                        top: 0;
                        left: 0;
                    }
                }
            }                                
        }
    }

    .missing-points {
        overflow: hidden;
        background: rgba(97,97,97,0.8);
        color: #fff;
        font-size: 14px;
        padding: 12px 34px 12px 20px;
        border-radius: 100px;
        position: absolute;
        top: 12px;
        right: 20px;


        span::after {
            content: "";
            display: block;
            width: 20vw;
            height: 20vw;
            box-sizing: border-box;
            border: 5px solid rgb(248,19,91);
            border-radius: 50%;                                
            position: absolute;
            top: 50%;
            left: 50%;                
            transform: translate(-50%, -50%) scale(0);                                
            animation-duration: .8s;
            animation-iteration-count: 1;
        }

        i {
            width:24px;
            height: 24px;
            display: inline-block;
            vertical-align:middle;
            margin-left:3px;
            right: 6px;
            top:10px;
        position: absolute;                
        animation-timing-function: ease;
        animation-duration: .8s;
        animation-iteration-count: 1;

        }
    }

    .data-wrap {
        transition: all 1.5s ease-out !important;  
        padding-top: 19px;
        margin: 0 24px;
        border-top: solid 1px #d9d9d9;

        .category {
            font-size:16px;
            color:#a3a3a3;
            margin-bottom:5px;
        }
    }

    /*** Transition effects ***/
    &.itemfX-enter{       
        transition: all 1s ease-out !important;  
        box-shadow:2px 2px 4px 0 rgba(0,0,0,0); 
        
        .data-wrap, .img-wrap {            
            opacity: 0;          
        }

        .missing-points {
            transform: scale(0);
        }           
                
        &::after {
        transform: translate(0%, 0);
        }                  
    }

    &.itemfX-enter-to{       
        .data-wrap,.img-wrap {
            transition: all 1s ease-out; 
            opacity: 1;  
        }            

        .missing-points {
            transition: transform 1s;
            transition-delay: .7s;
            transform: scale(1);
        }           
    }

    &.itemfX-leave-to {
        transition: all 0s;
        display: none;
    }

}


/*** Product over effects ***/
.productOver {        
    .hover {
        top: 0;
        right: 0;
        width: 100%;
        height: 100%;
        border-radius:0;

        > div {
            opacity: 1;                
        }
    }

    .buy-icon {            
        svg > g > circle {
            fill:#fff;
        } 

        svg .bag {
            fill:#43c9f5;
        }
    }

    .missing-points  {
        span::after {
                animation-name: rebound; 
        }

        i {
            animation-name: rebound-coin;            
        }
    }
}


/*** Medias query ***/
@media (max-width: 1080px) {
    .img-wrap {       
        min-height: 10.3rem;
    }
}


/*** Animations ***/
@keyframes rebound-coin {
	0%, 20%, 50%, 80%, 100% {transform: translateY(0);}
	40% {transform: translateY(-8px);}
	60% {transform: translateY(-3px);}
}

@keyframes rebound {    
	0%  {background:rgba(248,19,91,.8); opacity: 1;}	
	100% {transform: translate(-50%, -50%) scale(1); opacity: 0;}
}
    
</style>
