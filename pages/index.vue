<template>
  <div class="index-page">
    <a class="logo-link" href="#">Logo Logo</a>
    <div class="social-wrapper">
      <a class="social-link" href="#">Inst</a>
      <div class="social-spacer"></div>
      <a class="social-link" href="#">Fb</a>
    </div>
    <nav class="main-nav">
      <div
        class="main-nav__icon"
        :class="{ opened: menuOpened }"
        @click="menuOpened = !menuOpened"
      ></div>
      <ul
        class="main-nav__list"
        :class="{ opened: menuOpened }"
      >
        <li class="main-nav__item">
          <a class="nav-link" href="#">Commercial</a>
        </li>
        <li class="main-nav__item">
          <a class="nav-link" href="#">Editorial</a>
        </li>
        <li class="main-nav__item">
          <a class="nav-link" href="#">Reportage</a>
        </li>
        <li class="main-nav__item">
          <a class="nav-link" href="#">Meet me</a>
        </li>
      </ul>
    </nav>

    <swiper
      class="swiper"
      ref="swiper"
      :options="swiperOption"
      :slideChange="slideChange"

      content="Drag me"
      v-tippy="{followCursor : true, offset : '50, 0', theme: 'light'}"
    >
      <swiper-slide ref="slide-0">
        <span class="slide-text">Ink Lingerie</span>
      </swiper-slide>
      <swiper-slide ref="slide-1">
        <span class="slide-text">Ink Lingerie</span>
      </swiper-slide>
      <swiper-slide ref="slide-2">
        <span class="slide-text">Ink Lingerie</span>
      </swiper-slide>
    </swiper>

    <div class="photo-gallery scene">
      <img
        class="photo-item photo-item--prev layer"
        :src="require('@/assets/images/' + imagesForSlider[1])"
        alt="photo-item--prev"
        data-speed="10"
      />
      <img
        class="photo-item photo-item--active layer"
        :src="require('@/assets/images/' + imagesForSlider[0])"
        alt="photo-item--active"
        data-speed="20"
      />
      <img
        class="photo-item photo-item--next layer"
        :src="require('@/assets/images/' + imagesForSlider[2])"
        alt="photo-item--next"
        data-speed="40"
      />
    </div>

    <div class="bg-vector-wrapper">
      <svg class="bg-vector" width="610" height="728" viewBox="0 0 610 728" fill="none" xmlns="http://www.w3.org/2000/svg">
        <path class="bg-vector__path" d="M139.416 31.4647C-159.248 309.376 101.471 367.764 214.964 1C336.277 136.37 767.08 317.52 345.08 103.2C594.544 524.358 643.701 254.041 589.613 727.477" stroke="#2828BD"/>
      </svg>
    </div>

  </div>
</template>

<script>
import Vue from "vue";
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'

import VueTippy, { TippyComponent } from "vue-tippy";
Vue.use(VueTippy);
Vue.component("tippy", TippyComponent);
import "tippy.js/themes/light.css";

export default {
  components: [
    Swiper,
    SwiperSlide
  ],
  data: () => ({
    menuOpened: false,
    imagesForSlider: [
      'image1.png',
      'image2.png',
      'image3.png',
    ],
    swiperOption: {
      slidesPerView: 2,
      spaceBetween: 30,
      centeredSlides: true,
      loop: true,
      keyboard: {
        enabled: true,
      },

    },
    activeSlide: 1
  }),
  methods: {
    slideChange() {
      this.activeSlide = 0
    }
  },
  computed: {
    currentSlide() {
      return this.$refs.swiper.$swiper.realIndex
    },
  },
  mounted() {
    function parallax(event) {
      this.querySelectorAll('.layer').forEach(layer => {
        let speed = layer.getAttribute('data-speed');
        layer.style.transform = `translate(${event.clientX * speed / 1000}px, ${event.clientY * speed / 1000}px)`
      });
    }
    document.addEventListener('mousemove', parallax)
  }
}
</script>

<style lang="scss" scoped>

  .index-page {
    position: relative;

    .logo-link {
      position: absolute;
      top: 40px;
      left: 48px;
      font-style: normal;
      font-weight: bold;
      font-size: 16px;
      line-height: 16px;
      text-decoration: none;
      color: #000000;
      z-index: 5;
    }

    .social-wrapper {
      position: absolute;
      bottom: 47px;
      left: 48px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      font-family: TT Travels, sans-serif;
      font-style: normal;
      font-weight: 300;
      font-size: 12px;
      line-height: 14px;
      text-align: right;
      letter-spacing: 0.02em;
      text-transform: capitalize;
      z-index: 5;

      .social-link {
        text-decoration: none;
        color: #000000;
      }

      .social-spacer {
        width: 56px;
        height: 1px;
        margin-left: 8px;
        margin-right: 8px;
        background: #393939;
        opacity: 0.24;
      }
    }

    .main-nav {
      position: absolute;
      top: 40px;
      right: 48px;
      display: flex;
      flex-direction: column;
      align-items: flex-end;
      font-family: TT Travels, sans-serif;
      font-style: normal;
      font-weight: 300;
      font-size: 11px;
      line-height: 13px;
      text-align: right;
      letter-spacing: 0.02em;
      text-transform: capitalize;
      z-index: 5;

      &__icon {
        position: relative;
        width: 20px;
        height: 20px;
        margin-bottom: 20px;
        display: none;

        &::before {
          position: absolute;
          content: "";
          left: 0;
          top: 6px;
          width: 20px;
          height: 1px;
          background: #000000;
          transition: all 0.3s;
        }

        &::after {
          position: absolute;
          content: "";
          left: 0;
          bottom: 6px;
          width: 20px;
          height: 1px;
          background: #000000;
          transition: all 0.3s;
        }
      }

      &__icon.opened{
        &::before {
          top: 10px;
          transform: rotate(45deg);
        }

        &::after {
          bottom: 9px;
          transform: rotate(-45deg);
        }
      }

      &__list {
        margin: 0;
        padding: 0;
        list-style: none;
      }

      &__item {
        margin-bottom: 10px;
      }

      .nav-link {
        text-decoration: none;
        color: #000000;
      }
    }

    .swiper {
      height: 100vh;
      z-index: 4 !important;

      .swiper-slide {
        display: flex;
        justify-content: center;
        align-items: center;
        font-family: Schnyder Cond XL Demi;
        font-size: 126px;
        line-height: 108px;
        text-transform: uppercase;
        color: #580300;

        .slide-text {
          transition: color 0.5s;
        }
      }

      .swiper-slide-prev > .slide-text {
        transform: rotate(-1.5deg);
        transform-origin: right bottom;
        -webkit-text-stroke: 0.8px black;
        color: transparent;
      }

      .swiper-slide-next > .slide-text {
        transform: rotate(1.5deg);
        transform-origin: left bottom;
        -webkit-text-stroke: 0.8px black;
        color: transparent;
      }
    }

    .photo-gallery {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      z-index: 2;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;

      .photo-item {
        background-color: #eeeeee;
        object-fit: cover;

        &--prev {
          width: 238px;
          height: 331px;
          transform: rotate(1.1deg);
          position: relative;
          top: -40px;
          right: 15px;
        }

        &--active {
          width: 476px;
          height: 702px;
          transform: rotate(1.5deg);
        }

        &--next {
          width: 345px;
          height: 238px;
          transform: rotate(2.03deg);
          position: relative;
          top: 140px;
          left: -50px;
        }
      }
    }

    .bg-vector-wrapper {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: start;
      z-index: 0;

      .bg-vector{
        width: 608px;
        height: 726px;
      }

      .bg-vector__path {
        stroke-dasharray: 2000px;
        stroke-dashoffset: 2000px;
        animation: dash 15s linear infinite;
      }

      @keyframes dash {
        0% {
          stroke-dashoffset: 2000px;
        }
        50% {
          stroke-dashoffset: 0;
        }
        100% {
          stroke-dashoffset: 2000px;
        }
      }

    }

  }

  @media (max-width: 1024px) {
    .index-page {

      .logo-link {
        top: 27px;
        left: 32px;
      }

      .social-wrapper {
        bottom: 32px;
        left: 32px;
      }

      .main-nav {
        top: 27px;
        right: 32px;
      }

      .swiper {
        .swiper-slide {
          font-size: 96px;
          line-height: 83px;
        }
      }

      .photo-gallery {
        .photo-item {

          &--prev {
            width: 163px;
            height: 226px;
          }

          &--active {
            width: 359px;
            height: 530px;
          }

          &--next {
            width: 234px;
            height: 162px;
          }
        }
      }

      .bg-vector-wrapper {
        .bg-vector{
          width: 506px;
          height: 605px;
        }
      }
    }
  }

  @media (max-width: 768px) {
    .index-page {

      .logo-link {
        top: 27px;
        left: 32px;
      }

      .social-wrapper {
        bottom: 32px;
        left: 32px;
      }

      .main-nav {
        top: 27px;
        right: 32px;

        &__icon {
          display: block;
        }

        &__list {
          position: relative;
          right: -300px;
          transition: all 0.3s;
        }

        &__list.opened {
          right: 0;
        }

      }

      .photo-gallery {
        .photo-item {

          &--prev {
            width: 163px;
            height: 226px;
          }

          &--active {
            width: 359px;
            height: 530px;
          }

          &--next {
            width: 234px;
            height: 162px;
          }
        }
      }

      .bg-vector-wrapper {
        .bg-vector{
          width: 506px;
          height: 605px;
        }
      }
    }
  }

  @media (max-width: 414px) {
    .index-page {

      .logo-link {
        top: 33px;
        left: 24px;
      }

      .social-wrapper {
        bottom: 24px;
        left: 24px;
      }

      .main-nav {
        top: 33px;
        right: 24px;
      }

      .swiper {
        .swiper-slide {
          font-size: 48px;
          line-height: 41px;
        }
      }

      .photo-gallery {
        .photo-item {

          &--prev {
            display: none;
          }

          &--active {
            width: 273px;
            height: 403px;
          }

          &--next {
            display: none;
          }
        }
      }

      .bg-vector-wrapper {
        .bg-vector{
          width: 392px;
          height: 493px;
        }
      }
    }
  }

  @media (max-width: 375px) {
    .index-page {

      .logo-link {
        top: 16px;
        left: 20px;
      }

      .social-wrapper {
        bottom: 20px;
        left: 20px;
      }

      .main-nav {
        top: 16px;
        right: 20px;
      }

      .swiper {
        .swiper-slide {
          font-size: 44px;
          line-height: 38px;
        }
      }

      .photo-gallery {
        .photo-item {

          &--active {
            width: 250px;
            height: 368px;
          }
        }
      }

      .bg-vector-wrapper {
        .bg-vector{
          width: 339px;
          height: 429px;
        }
      }
    }
  }
</style>
