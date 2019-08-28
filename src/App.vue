<template>
   <div id="app">
      <b-jumbotron>
       <template slot="header">{{title}}</template>

        <template slot="lead">
          Welcom to my portfolio
        </template>

        <hr class="my-4">
       </b-jumbotron> 
    
       <b-nav pills>
           <b-nav-item active to="/">Homes</b-nav-item>
           <b-nav-item to="/about">About </b-nav-item>
        </b-nav>
 
        <transition  
          name="fade"
          mode="out-in"
          @beforeLeave="beforeLeave"
          @enter="enter"
          @afterEnter="afterEnter">
         <router-view></router-view>
        </transition>
        <div id="footer-nav" class="nav-bars">
            
        </div>
    </div>
</template>

<script>

  import * as types from './store/types';

export default {
  name: "App",
  data() {
    return {
        title:'My portfolio',
        prevHeight: 0
    };
  },
  methods: {
    beforeLeave(element) {
      this.prevHeight = getComputedStyle(element).height;
    },
    enter(element) {
      const { height } = getComputedStyle(element);

      element.style.height = this.prevHeight;

      setTimeout(() => {
        element.style.height = height;
      });
    },
    afterEnter(element) {
      element.style.height = 'auto';
    },
  }
};
</script>


<style lang="scss">


#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;

  .nav.nav-pills {
    justify-content: center;
    background: cornflowerblue;
    width: 100%;
    padding: 10px;
    color: white;

    a {
      background: transparent;
      color: white;
      text-decoration: none;
      &:hover,&:active,&:focus{
        background: #2c3e50;
      }
    }
  }

  #header-nav {
    top: 0;
    left: 0;
  }

  #footer-nav {
    bottom: 0;
    left: 0;
  }

  .fade-enter-active,
  .fade-leave-active {
    transition-duration: 0.3s;
    transition-property: opacity;
    transition-property: height, opacity;
    transition-timing-function: ease;
    overflow: hidden;
 }
}
</style>