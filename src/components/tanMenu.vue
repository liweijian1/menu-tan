<template>
  <div>
    <div class="menu-bg" ref="menuHome" @click="tggMenu">
      <img :src="imgURL">
    </div>
    <div class="menu-item" ref="menuItem" v-for="(item,index) in menuItems" :key="item.src" :id="item.name" @click="clickMenu(item,index)">
      <img :src="item.src">
    </div>
  </div>
</template>

<script>// eslint-disable-next-line
  /* eslint-disable */
    export default {
        name: "tanMenu",
        props:{
          imgURL:{
            default:require('../assets/menu.png')
          },
          width: {
            default: 50,
          },
          menuBg:{
            default:'white'
          },
          itemBg:{
            default:'white'
          },
          menuItems: {
            type: Array,
          },
          basedistance:{
            default:150,
          }
        },
        data(){
          return{
            openFlag:false,
            operators:['+','+'],
          }
        },
        mounted(){
          this.$refs.menuHome.style.background = this.menuBg;
          this.menuItems.forEach((item) => {
            let el = document.getElementById(item.name);
            el.style.background = this.itemBg;
          });
          this.$refs.menuHome.style.right = '20px';
          this.$refs.menuHome.style.bottom = '20px';
          this.menuItems.forEach((item) => {
            let el = document.getElementById(item.name);
            el.style.right = '26px';
            el.style.bottom = '26px';
          });
          this.operators = ['-', '-'];
        },
         methods:{
            tggMenu(){
              if(!this.openFlag){
                  this.menuItems.forEach((item,index) =>{
                    this.toggleMenuTransition(item.name,index,false)
                });
                 this.$refs.menuHome.style.transform='rotate(360deg)';
              }
              else{
                this.menuItems.forEach((item,index) => {
                  this.toggleMenuTransition(item.name,index,true)
                });
                this.$refs.menuHome.style.transform='rotate(0)';
              }
              this.openFlag = !this.openFlag;
            },
           toggleMenuTransition(name,index,revert){
               let allArea = 90 / (this.menuItems.length - 1);
               let axisx = Math.sin((this.menuItems.length - 1 - index) * allArea * 2 * Math.PI / 360);
               let axisy = Math.cos((this.menuItems.length - 1 - index) * allArea * 2 * Math.PI / 360);
               let el = document.getElementById(name);
               let that = this;
               if(!revert){
                 setTimeout(function(){
                   el.style.transitionDuration = '200ms';
                   el.style.transform = `translate(${that.operators[0]}${that.basedistance*axisx}px,${that.operators[1]}${that.basedistance*axisy}px)`;
                 },index * 100)
               }else{
                 el.style.transitionDuration = '200ms';
                 el.style.transform = `translate(0,0)`;
               }
           },
           clickMenu(item, index){
              this.$emit('clickMenu',item,index)
           }
         }

    }
</script>

<style scoped>
  .menu-bg{
    position: absolute;
    top:87%;
    width: 50px;
    height: 50px;
    line-height: 50px;
    cursor: pointer;
    border: 3px solid #efefef;
    border-radius: 50%;
    text-align: center;
    box-shadow: aliceblue 1px 1px 1px;
    transition-duration:400ms;
    z-index: 100;
  }
  .menu-item{
    position: absolute;
    border-radius: 50%;
    width: 30px;
    height:30px;
    line-height: 30px;
    z-index: 99;
    border: #efefef 3px solid;
    text-align: center;
    box-shadow: aliceblue 1px 1px 1px;
    transition-duration:400ms;
  }
   img{
     width: 50%;
     transform: translate(-5%,20%);
   }
</style>
