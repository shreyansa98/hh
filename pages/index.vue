<template>
    <main>
    <div id="landing-header">
 		<h1>Welcome to Handmade Happiness!</h1>
		<a href="/hh/home" class="btn btn-lg btn-outline-light">Home</a> 
    </div>
    
    <ul class="slideshow">
      <li></li>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  </main>
</template>

<style>
body { 
   background-color: #000; 
 }

#landing-header {
  z-index: 1;
  position: relative;
  text-align: center;
  padding-top: 40vh;
}

#landing-header h1 {
  color: #fff;
}
 
.slideshow { 
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  z-index: 0;
  list-style: none;
  margin: 0;
  padding: 0;
}

.slideshow li { 
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
  background-size: cover;
  background-position: 50% 50%;
  background-repeat: no-repeat;
  opacity: 0;
  z-index: 0;
  animation: imageAnimation 25s linear infinite; 
}

.slideshow li:nth-child(1) { 
  background-image: url(https://cdn.pixabay.com/photo/2020/06/20/14/12/muffin-5321148_960_720.jpg); 
}
.slideshow li:nth-child(2) { 
  background-image: url(https://cdn.pixabay.com/photo/2015/05/07/15/08/pastries-756601_960_720.jpg);
  animation-delay: 5s; 
}
.slideshow li:nth-child(3) { 
  background-image: url(https://cdn.pixabay.com/photo/2013/09/18/18/24/chocolate-183543_960_720.jpg);
  animation-delay: 10s; 
}
.slideshow li:nth-child(4) { 
  background-image: url(https://cdn.pixabay.com/photo/2015/03/26/09/39/cupcakes-690040_960_720.jpg);
  animation-delay: 15s; 
}
.slideshow li:nth-child(5) { 
  background-image: url(https://cdn.pixabay.com/photo/2020/04/20/17/42/chocolate-pudding-5069214_960_720.jpg);
  animation-delay: 20s; 
}

@keyframes imageAnimation { 
  0% { 
    opacity: 0; 
    animation-timing-function: ease-in;
  }
  10% {
    opacity: 1;
    animation-timing-function: ease-out;
  }
  20% {
    opacity: 1
  }
  30% {
    opacity: 0
  }
}

/* Older browser support - .no-cssanimations class added by modernizr */
.no-cssanimations .slideshow li {
	opacity: 1;
}
</style>
