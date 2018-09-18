<template>
  <div class="tan-box">
    <tan-menu :menuItems="menuItems" @clickMenu="clickMenu"></tan-menu>
  </div>
</template>

<script>// eslint-disable-next-line
/* eslint-disable */
    import TanMenu from "./tanMenu";
export default {
        name: "index",
  components: {TanMenu},
  data() {
    return {
      menuItems: [
        {name: 'menu1', src: require('../assets/emoji.png')},
        {name: 'menu2', src: require('../assets/cart.png')},
        {name: 'menu3', src: require('../assets/folder.png')},
        {name: 'menu4', src: require('../assets/home.png')},
        {name: 'menu5', src: require('../assets/my.png')},
      ]
    }
  },
  methods:{
          clickMenu(item,index){
            console.log(1111)
          }
  }
}
</script>

<style scoped>
  .tan-box{
    position: relative;
    left: 45%;
    border:1px solid #9999;
    width: 300px;
    height: 500px;
  }
</style>
