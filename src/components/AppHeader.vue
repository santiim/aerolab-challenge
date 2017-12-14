<template>
    <section class="app-header">    
        <header>
            <div class="container">
                <div class="logo">
                    <a href="/" >                         
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 45 42.83"> <path class="svg-logo-path" d="M35.66,0.48c-0.26-0.46-0.85-0.61-1.3-0.35l-15.59,9c-0.35,0.2-0.54,0.61-0.46,1.02L23.6,36l-0.79,0.89 c-1.33,1.49-2.45,2.3-4.58,2.3c-2.39,0-3.52-1.26-5.29-3.49c-2.12-2.66-4.77-5.97-11.19-5.97H1.59C0.71,29.73,0,30.44,0,31.32 c0,0.88,0.71,1.59,1.59,1.59h0.16c4.9,0,6.75,2.32,8.71,4.78c1.75,2.2,3.74,4.68,7.78,4.68c3.49,0,5.4-1.62,6.96-3.37l5.73-6.46 c0,0,13.63-15.37,13.63-15.37c0.27-0.31,0.32-0.75,0.11-1.11L35.66,0.48z"></path> </svg>
                    </a>            
                </div>
                <div class="user-data">
                    <span class="name">{{ userName }}</span>                    
                    <div class="wrap-points" :class="{ showDiscount: showDiscount }">
                        <span class="points">{{ userPoints }} </span>
                        <span class="discount" :show="showDiscount"  >-{{ discount }}</span>                               
                        <span class="icon">                        
                            <svg  viewBox="0 0 34 34" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"><defs><filter x="-9.1%" y="-9.1%" width="128.3%" height="128.3%" filterUnits="objectBoundingBox" id="filter-1"><feOffset dx="2" dy="2" in="SourceAlpha" result="shadowOffsetOuter1"></feOffset><feGaussianBlur stdDeviation="2" in="shadowOffsetOuter1" result="shadowBlurOuter1"></feGaussianBlur><feColorMatrix values="0 0 0 0 0   0 0 0 0 0   0 0 0 0 0  0 0 0 0.1 0" type="matrix" in="shadowBlurOuter1" result="shadowMatrixOuter1"></feColorMatrix><feMerge><feMergeNode in="shadowMatrixOuter1"></feMergeNode><feMergeNode in="SourceGraphic"></feMergeNode></feMerge></filter><radialGradient cx="50%" cy="50%" fx="50%" fy="50%" r="68.6284858%" id="radialGradient-2"><stop stop-color="#FFCF00" offset="0%"></stop><stop stop-color="#F7AE15" offset="100%"></stop></radialGradient></defs><g id="Page-1" stroke="none" stroke-width="1" fill="none" fill-rule="evenodd"><g id="Catalog-pg1" transform="translate(-609.000000, -731.000000)"><g id="products" transform="translate(132.000000, 622.000000)"><g id="line-1"><g id="product-card-hover" filter="url(#filter-1)" transform="translate(300.000000, 0.000000)"><g id="money" transform="translate(71.000000, 100.000000)"><g transform="translate(108.000000, 11.000000)"><g><circle id="Oval-Copy-3" fill="url(#radialGradient-2)" cx="13" cy="13" r="13"></circle><path d="M13,3.0952381 C7.54580357,3.0952381 3.0952381,7.54657738 3.0952381,13 C3.0952381,18.4541964 7.54657738,22.9047619 13,22.9047619 C18.4541964,22.9047619 22.9047619,18.4534226 22.9047619,13 C22.9047619,7.54580357 18.4534226,3.0952381 13,3.0952381 Z M13,21.7440476 C8.17850893,21.7440476 4.25595238,17.8214911 4.25595238,13 C4.25595238,8.17850893 8.17850893,4.25595238 13,4.25595238 C17.8214911,4.25595238 21.7440476,8.17850893 21.7440476,13 C21.7440476,17.8214911 17.8214911,21.7440476 13,21.7440476 Z" id="Shape" fill="#F8B013" fill-rule="nonzero"></path><path d="M13,5.2962963 C8.76834769,5.2962963 5.2962963,8.76956614 5.2962963,13 C5.2962963,17.2316523 8.76956614,20.7037037 13,20.7037037 C17.2316523,20.7037037 20.7037037,17.2304339 20.7037037,13 C20.7037037,8.76834769 17.2304339,5.2962963 13,5.2962963 Z M13,19.5245654 C9.40233107,19.5245654 6.47543462,16.5976689 6.47543462,13 C6.47543462,9.40233107 9.40233107,6.47543462 13,6.47543462 C16.5976689,6.47543462 19.5245654,9.40233107 19.5245654,13 C19.5245654,16.5976689 16.5976689,19.5245654 13,19.5245654 Z" id="Shape" fill="#F8B013" fill-rule="nonzero"></path></g></g></g></g></g></g></g></g></svg>
                        </span>
                    </div>
                </div>            
            </div>  
        </header>
        <div class="top-image blur">            
            <div class="container">            
                <h1>Electronics</h1>
            </div>              
        </div>          
    </section>
</template>


<script>
import { EventBus } from '../event-bus.js';

export default {
    name:'app-header',

    data () {
        return {
            userPoints:'',
            showDiscount:false,
            discount:'',
        }        
    },


    // PROPERTIES
    // -----------
    props: {
        userName: String,
    },


    // METHODS
    // -----------
    methods : {

        // Control animation when redeeming a product
        descountPoint(points) {
            if (points > 0) {
                this.showDiscount = true;                
                this.discount = points;
                this.playCashSound();
                setTimeout(() => {
                    this.showDiscount = false;    
                }, 3000);                
            }
        },

        // Emit sound 
        playCashSound() {            
            var audio = new Audio('http://bypleds.com.ar/sounds/cashFx.mp3');                    
            audio.play();
        }
    },

 
    // MOUNTED
    // -----------
    mounted () {
        EventBus.$on('user-points', (points) => {
            this.descountPoint(this.userPoints - points);
            this.userPoints = points;
        });    
    }
}

</script>


<style lang="postcss" scoped>

    header {
        position: fixed;
        transform: translateY(0);
        width: 100%;
        height: 80px;
        background: #fff;
        z-index: 9;
        top: 0;
        left: 0;
        box-shadow: 0 0 2px 0 rgba(0,0,0,.12), 0 -1px 12px 0 rgba(0,0,0,.2);
        transition: all .5s;

        .container {
            display: flex;            
            justify-content: space-between;            
            height: 100%;
        }

        .logo {
            align-self:center;
            a {                
                position: relative;
                display: block;
                width: 36px;
                height: 26px; 
                svg {
                    fill: #ff7b00;                    
                }                           
            }
        }

        .user-data {
            align-self:center;
            font-size: 24px;            

            .wrap-points {
                position: relative;
                display: inline-block;
                background: #ededed;
                border-radius:20.5px;
                border-radius:2rem;
                padding:10px 13px;
                margin-left:18px;

                .points {
                    transform: scale(1);
                }

                .discount {
                    position: absolute;
                    text-align: center;
                    font-weight: 700;
                    color: #f54370;
                    font-size: 33px;
                    text-align: center;
                    left: 50%;
                    transform-origin:0 0;                    
                    top: 50%;
                    text-shadow: 1px 2px 2px rgba(0,0,0,0.5);                                        
                    opacity: 0;
                }

                .icon {      
                    display: inline-block;
                    width: 24px;
                    height: 24px;
                    vertical-align: middle;          
                    a {
                        display: block;
                        width: 39px;
                        height: 36px;  
                    }                
                }


                /*** Effect when changing a product ***/
                &.showDiscount {

                    .points {
                        animation: pointsFx 1s linear; 
                        animation-delay:.3s;
                    }

                    .discount {
                        animation: discountFx .5s linear; 
                        animation-delay:.5s;
                    }
                }
            }        
        }
    }

    .top-image {     
        position: relative;   
        min-height: 412px;
        max-height: 470px;
        background: #6ee8ff url('../assets/img/header-x1.jpg') no-repeat;
        background-position: top;        
        background-size: cover;
                                
        .container {        
            h1 {                            
                color: #fff;
                position: absolute;
                bottom:50px;
            }
        }
    }    


    /*** Animations ***/
    @keyframes discountFx {
        0% {
            opacity: 1;
              transform:  scale(0)
                          translate(-50%,-50%);
            }
        10% {                                
              transform: scale(1)
                         translate(-50%,-50%);
            }     
        70% {                          
             opacity: 1;
             transform: translate(-50%,-50%);
            }
        100% {
            transform: translate(-50%,-300%);
            opacity: 0;
            }        
    }
    
    @keyframes pointsFx {
        0% {
            color:#f54370;
            opacity: 0;                        
            }

        100% {            
            opacity: 1;            
            }        
    }


    /*** Responsive top image ***/
    @media 
    only screen and (-webkit-min-device-pixel-ratio: 2),
    only screen and (min--moz-device-pixel-ratio: 2),
    only screen and (min-device-pixel-ratio: 2),
    only screen and (-webkit-min-device-pixel-ratio: 2),
    only screen and (min-resolution: 192dpi),
    only screen and (min-resolution: 2dppx) {
        .top-image {            
            background: #6ee8ff url('../assets/img/header-x2.jpg') no-repeat;
        }    
    }



    
</style>


