<template>
    <div v-if="checkSun" class="sun">
      <div class="sun-core"></div>
      <div class="sun-ray sun-ray-1"></div>
      <div class="sun-ray sun-ray-2"></div>
      <div class="sun-ray sun-ray-3"></div>
      <div class="sun-ray sun-ray-4"></div>
      <div class="sun-ray sun-ray-5"></div>
      <div class="sun-ray sun-ray-6"></div>
      <div class="sun-ray sun-ray-7"></div>
      <div class="sun-ray sun-ray-8"></div>
    </div>
    <div v-else class>
         <div class="stars">
            <div class="stars_1"></div>
            <div class="stars_2"></div>
            <div class="stars_3"></div>
            <div class="stars_4"></div>
            <div class="stars_5"></div>
            <div class="stars_6"></div>
            <div class="stars_7"></div>
            <div class="stars_8"></div>
            <div class="stars_9"></div>
            <div class="stars_10"></div>
          </div>
    </div>
</template>

<script>
export default {
      props: {checkSun: { type: Boolean, default: () => 0, required: false },
        
          },
         
  data() {
    return {

    }
  },
}
</script>

<style>
    .stars {
    position: relative;
    overflow: hidden;
    height: 350px;
    margin-bottom: -350px;
}
.stars_1, .stars_2, .stars_3, .stars_4, .stars_5, .stars_6, .stars_7,.stars_8 {
    position: absolute;
    top: 0;
 
    width: 20px;
    height: 20px; 
    opacity: 0%;  
    background: url('/images/star1.svg');  
    -webkit-animation: stars 5s linear infinite;
    animation: stars 5s linear infinite;
    background-repeat: no-repeat;
    z-index: 10;
}
.stars_1 {
    top: 12px;
    left: 15px;
}
.stars_2 {
    background-image: url('/images/star2.svg');
    /* background-position: 100px 100px; */
    -webkit-animation-delay: 1s;
    animation-delay: 1s;
    animation-delay: 1s;
    top: 20px;
    right: 21px;
    width: 20px;
}
.stars_3 {
    background-image: url('/images/star3.svg');
    top: 115px;
    right: 17px;
    -webkit-animation-delay: 3s;
    animation-delay: 3s;
}
.stars_4 {
    background-image: url('/images/star4.svg');
   top: 58px;
   right: 84px;
   -webkit-animation-delay: 1.5s;
   animation-delay: 1.5s;
}
.stars_5 {
   background-image: url('/images/star5.svg');
   right: 15px;
   top: 200px;
   -webkit-animation-delay: 4s;
   animation-delay: 4s;
}
.stars_6 {
    background-image: url('/images/star6.svg');
    left: 15px;
    top: 240px;
    -webkit-animation-delay: 3s;
    animation-delay: 3s;
}
.stars_7 {
    background-image: url('/images/star7.svg');
    right: 129px;
    top: 230px;
    -webkit-animation-delay: 3s;
    animation-delay: 3s;
}
.stars_8 {
    background-image: url('../assets/');
    left:10px;
    top: 120px;
    -webkit-animation-delay: 3s;
    animation-delay: 3s;
}
</style>