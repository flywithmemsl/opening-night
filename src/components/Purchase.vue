<template lang="pug">
  transition
    .modal
      .modal-inner
        .modal-close(@click="onClose")
        .title
          | SELECT A SOURCE TO START WATCHING
        .buttons
          a.button-1(target="_blank" href="https://www.amazon.com/Opening-Night-Isaac-Rentz/dp/B072JG9S7F/ref=sr_1_3?ie=UTF8&qid=1496927045&sr=8-3&keywords=opening+night")
            .button-inner
          a.button-2(target="_blank" href="https://itunes.apple.com/us/movie/opening-night/id1230733174")
            .button-inner
          a.button-3(target="_blank" href="https://play.google.com/store/movies/details/Opening_Night?id=5vO1bfhLwxA")
            .button-inner
          a.button-4(target="_blank" href="https://www.vudu.com/movies/#!content/864420/Opening-Night")
            .button-inner

        .available
          | Also available on <span> Playstation & XBox </span>
</template>
<script>
  export default {
    name: "PurchaseComponent",

    methods: {
      onClose: function () {
        this.$emit('close');
      }
    }
  }
</script>

<style lang="scss"  rel="stylesheet/scss">
  .v-enter-active, .v-leave-active {
    transition: opacity 0.3s ease;

    .modal-inner {
      transition: transform 0.3s ease;
    }
  }
  .v-enter, .v-leave-active {
    opacity: 0.01;

    .modal-inner {
      transform: translate3d(0,-100%,0);
    }
  }

  .modal {
    background: rgba(0,0,0,0.4);

    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;

    z-index: 10000;

    display: flex;
    flex-flow: column nowrap;
    justify-content: center;
    align-items: center;

    &-hidden {
      display: none;
    }

    &-close {
      background: url('~assets/images/cross-modal.svg') no-repeat center center / contain;
      width: 17px;
      height: 15px;

      position: absolute;
      top: 18px;
      right: 18px;

      cursor: pointer;
    }

    &-inner {
      background-image: linear-gradient(-180deg, #FFDC39 0%, #FCC63B 100%);
      box-shadow: 0px 2px 13px 0px rgba(0,0,0,0.50);
      border-radius: 3px;

      padding: 35px 43px 39px;

      display: flex;
      flex-flow: column nowrap;
      justify-content: center;
      align-items: center;

      position: relative;
    }

    .title {
      opacity: 0.66;
      font-size: 14px;
      color: #090909;
      letter-spacing: 1.75px;
      line-height: 22px;
      text-align: center;
    }

    .buttons {
      margin-top: 21px;
      width: 90%;
    }

    .button-1,
    .button-2,
    .button-3,
    .button-4 {
      background: #000000;
      padding: 0 52px;
      height: 68px;
      border-radius: 3px;

      display: flex;
      flex-flow: column nowrap;
      justify-content: center;
      align-items: center;

      transition: box-shadow 0.1s ease;
      will-change: box-shadow;

      &:hover {
        box-shadow: 0px 1px 2px 0px rgba(0,0,0,0.50);
      }
    }

    .button-2,
    .button-3,
    .button-4 {
      margin-top: 17px;
    }

    .button-1 .button-inner {
      background: url('~assets/images/amazon.png') no-repeat center center / contain;
      height: 70px;
      width: 217px;
    }

    .button-2 .button-inner {
      background: url('~assets/images/itunes.png') no-repeat center center / contain;
      height: 45px;
      width: 151px;
    }

    .button-3 .button-inner {
      background: url('~assets/images/googlePlay.png') no-repeat center center / contain;
      height: 54px;
      width: 155px;
    }

    .button-4 .button-inner {
      background: url('~assets/images/vudu.png') no-repeat center center / contain;
      height: 31px;
      width: 64px;
    }

    .available {
      margin-top: 13px;

      font-family: 'Open Sans', sans-serif;
      font-size: 12px;
      color: #000000;
      letter-spacing: 0.75px;
      line-height: 18px;
      text-align: center;

      span {
        display: block;
        font-weight: bold;
        font-size: 14px;
        color: #000000;
        letter-spacing: 0.87px;
      }
    }
  }


  @media (max-width: 425px) {
    .modal {
      &-inner {
        width: 100%;
        height: 100%;
        border-radius: 0;
        padding: 0;
      }

      .buttons {
        width: 90%;
      }
    }
  }
</style>
