<template lang="pug">
  .menu(v-bind:class="{ 'showedMenu': this.scrolled, 'showMenu': this.showMenu }")
    a.menu-logo(href="#")
      img(src="~assets/images/logo-small.png")
    .menu-list(v-bind:class="{ 'showedList': this.showMenu }")
      .menu-item(@click="onClickItem(SECTION_CAST)" v-bind:class="{'menu-active': currentSection == SECTION_CAST}") Cast
      .menu-item(@click="onClickItem(SECTION_REVIEWS)" v-bind:class="{'menu-active': currentSection == SECTION_REVIEWS}") Reviews
      .menu-item(@click="onClickItem(SECTION_CLIPS)" v-bind:class="{'menu-active': currentSection == SECTION_CLIPS}") Clips
      .menu-item(@click="onClickItem(SECTION_CONTEST)" v-bind:class="{'menu-active': currentSection == SECTION_CONTEST}") Contest
    .burger(@click="onClickBurger")
</template>

<script>
  import {TweenMax} from 'gsap';
  import ScrollToPlugin from 'gsap/src/uncompressed/plugins/ScrollToPlugin';

  import store from 'store/Store';


  export default {
    name: "MenuComponent",

    props: ['currentSection'],

    data: function() {
      return {
        scrolled: false,
        showMenu: false,

        "SECTION_CAST":     store().SECTION_CAST,
        "SECTION_REVIEWS":  store().SECTION_REVIEWS,
        "SECTION_CLIPS":    store().SECTION_CLIPS,
        "SECTION_CONTEST":  store().SECTION_CONTEST
      }
    },

    methods: {
      handleScroll () {
        this.scrolled = window.scrollY > window.innerHeight;
      },

      onClickWatch: function () {
        this.$emit('watchOpen');
      },

      onClickBurger: function () {
        this.showMenu = !this.showMenu;
        if (this.showMenu)
          document.body.style.overflowY = 'hidden';
        else
          document.body.style.overflowY = 'scroll';
      },

      onClickItem: function (item) {
        if (store().isMobile || store().isTablet)
          this.onClickBurger();

        let pointTo = 0;
        switch (item) {
          case this.SECTION_CAST:     pointTo = 0; break;
          case this.SECTION_REVIEWS:  pointTo = store().sectionReviews.offsetTop; break;
          case this.SECTION_CLIPS:    pointTo = store().sectionClips.offsetTop; break;
          case this.SECTION_CONTEST:  pointTo = store().sectionContest.offsetTop; break;
        }

        if (store().isMobile || store().isTablet)
          window.scrollTo(0, pointTo);
        else
          TweenMax.to(window, .5, {scrollTo: pointTo});
        this.$emit('nav');
      }
    },

    mounted: function() {
      let raf =
        window.requestAnimationFrame ||
        window.webkitRequestAnimationFrame ||
        window.mozRequestAnimationFrame ||
        window.msRequestAnimationFrame ||
        window.oRequestAnimationFrame;

      let lastScrollTop = window.scrollY;

      let loop = () => {
        if (lastScrollTop != window.scrollY) {
          lastScrollTop = window.scrollY;
          // fire scroll function if scrolls vertically
          this.handleScroll();
        }
        raf(loop);
      };

      if (raf)
        loop();

      // window.addEventListener('scroll', this.handleScroll);
    }
  }
</script>

<style lang="sss"  rel="stylesheet/sass">
  .menu
    position: fixed
    width: 100%
    top: 0
    left: 0

    z-index: 9999

    background: rgba(10,10,10,0.90)
    box-shadow: 0px 2px 4px 0px rgba(0,0,0,0.50)

    display: flex
    flex-flow: row nowrap
    justify-content: space-between
    align-items: center

    padding: 0 30px
    height: 60px

    transform: translateY(-120%)
    transition: transform 0.3s ease
    will-change: transform

    &.showedMenu
      transform: translateY(0)

    &.showMenu
      width: 100%

    &-logo
      position: relative
      width: 119px

      img
        height: 71px
        position: absolute
        top: -25px
        z-index: 5

    &-list
      display: flex
      flex-flow: row nowrap
      justify-content: flex-end
      align-items: center
      flex: 1

      &.showedList
        display: flex

    &-item
      display: block
      font-family: 'Open Sans', sans-serif
      color: #D0D0D0
      line-height: 60px
      text-transform: uppercase
      padding: 0 20px
      cursor: pointer

    &-item.menu-active
      color: #FFFFFF
      font-weight: bold

    .watch
      margin-left: 38px
      font-family: 'Open Sans Hebrew Condensed', sans-serif
      background-image: linear-gradient(-182deg, #f45232 0%, #e52816 100%)
      box-shadow: 0px 3px 10px 0px rgba(79, 24, 91, 0.68)
      padding: 0 18px
      border-radius: 120px
      text-transform: capitalize
      font-weight: bold
      font-size: 18px
      color: #FFFFFF
      letter-spacing: 1.46px
      text-align: center
      line-height: 35px
      cursor: pointer

      position: relative
      overflow: hidden

      .text
        position: relative
        z-index: 4

      .bg-1,
      .bg-2
        position: absolute
        top: 0
        left: 0
        width: 100%
        height: 100%
        border-radius: 100px
        background: linear-gradient(-182deg, #f45232 0%, #e52816 100%)

      .bg-2
        background: linear-gradient(-182deg, #FF7340 0%, #F9412F 100%)
        opacity: 0.01
        transition: opacity 0.1s ease
        will-change: opacity

      &:hover .bg-2
        opacity: 0.99
</style>

<style  lang="scss" rel="stylesheet/scss">

  @media (max-width: 768px) {
    .menu {
      width: 0;
      left: initial;
      right: 0;
      background: transparent;
      box-shadow: none;
      transform: translate3d(0,0,0);

      .burger {
        background: url('~assets/images/burger.svg') no-repeat center center / contain;
        height: 28px;
        width: 36px;

        position: absolute;
        right: 22px;
        top: 20px;

        z-index: 5;

        cursor: pointer;
      }

      .watch,
      &-logo {
        display: none;
      }

      &-list {
        display: none;
        position: fixed;
        top: 0;
        left: 0;
        width: 100%;
        height: calc(100vh + 1px);
        background: #000;
        flex-flow: column nowrap;
        justify-content: center;
      }

      &-item {
        font-size: 36px;
        margin-top: 20px;
      }
    }
  }
</style>
