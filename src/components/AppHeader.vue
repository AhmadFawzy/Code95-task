<template>
  <div class="app-nav">
    <div class="lv1 d-flex justify-content-end align-items-center">
      <div>
        <i class="fab fa-twitter pointer mx-md-3 mx-2"></i>
        <i class="fab fa-whatsapp pointer mx-md-3 mx-2"></i>
      </div>
      <div class="lang-dropdown d-flex align-items-center flex-nowrap pointer mx-md-5 mx-3">
        <span class="text-nowrap">اللغة العربية</span>
        <i class="fas fa-sort-down"></i>
      </div>
    </div>

    <div class="lv2 d-sm-flex justify-content-between align-items-center position-relative">
      <div class="d-flex justify-content-between justify-content-sm-start align-items-center">
        <i @click="toggleSideNav" class="fas fa-bars d-block d-lg-none pointer mx-sm-4 mx-3"></i>
        <img src="../assets/mashora.png" alt="logo">
        <div class="nav-links d-none d-lg-flex align-items-lg-center">
          <router-link class="text-nowrap mx-lg-2" to="#">الصفحة الرئيسية</router-link>
          <router-link class="text-nowrap mx-lg-2" to="#">منتجاتنا</router-link>
          <router-link class="text-nowrap mx-lg-2" to="#">مقياس الاستدامة المالية</router-link>
          <router-link class="text-nowrap mx-lg-2" to="#">حول المقياس</router-link>
          <router-link class="text-nowrap mx-lg-2" to="#">من نحن</router-link>
          <router-link class="text-nowrap mx-lg-2" to="#">تواصل معنا</router-link>
          <router-link class="text-nowrap mx-lg-2" to="#">الاسئلة الشائعة</router-link>
        </div>
      </div>
      <div class="d-sm-flex align-items-center d-none">
        <span class="vertical"></span>
        <i class="fas fa-search pointer mx-lg-4 mx-sm-3 "></i>
        <span class="vertical "></span>
        <img class="h-50 mx-lg-4 mx-sm-3 " src="../assets/malya.png" alt="icon">
        <button class="px-5 ">تسجيل دخول</button>
      </div>
      <div v-if="sideNav" class="side_nav px-2 pt-4">
        <p class="text-end px-2 mb-4">
          <i @click="toggleSideNav" class="fas fa-times pointer"></i>
        </p>
        <p v-for="link in links" :key="link.name">
          <router-link :to="link.path">{{ link.name }}</router-link>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sideNav: false,
      links: [
        {name: 'الصفحة الرئيسية', path: '#'},
        {name: 'منتجاتنا', path: '#'},
        {name: 'مقياس الاستدامة المالية', path: '#'},
        {name: 'حول المقياس', path: '#'},
        {name: 'من نحن', path: '#'},
        {name: 'تواصل معنا', path: '#'},
        {name: 'الاسئلة الشائعة', path: '#'},
      ]
    }
  },
  methods: {
    toggleSideNav() {
      this.sideNav = !this.sideNav;
    }
  }
}
</script>

<style lang="scss">
  .app-nav {
    width: 100%;
    font-size: 12px;
    font-weight: bold;
    overflow: hidden;
    .lv1 {
      height: 50px;
      color: white;
      background-color: #0C2D75;
      .lang-dropdown {
        text-align: center;
        i {
          transform: scale(0.8);
          margin: 0 10px 0 0;
        }
      }
    }
    .lv2 {
      height: 65px;
      color: gray;
      border-bottom: 1px solid #EDEDED;
      div {
        &:nth-child(1) {
          height: 100%;
          i {
            transform: scale(1.5);
            color: #fff;
            padding: 6px 8px;
            border-radius: 3px;
            background-color: #abc4f2;
          }
          img {
            max-height: 100%;
            margin: 0 2vw 0 2vw;
          }
          .nav-links {
            a {
              color: gray;
              text-decoration: none;
            }
          }
        }
        &:nth-child(2) {
          height: 100%;
          .vertical {
            content: '';
            display: block;
            width: 1px;
            height: 100%;
            background-color: #EDEDED;
          }
          button {
            color: white;
            background-color: #66BDE1;
            border: none;
            height: 100%;
          }
        }
      }
      .side_nav {
        position: fixed;
        top: 0;
        width: 150px;
        height: 400px;
        background-color: #abc4f2;
        overflow-y: auto;
        z-index: 2;
        i {
          transform: scale(1.5);
          color: #abc4f2;
          padding: 6px 8px;
          border-radius: 3px;
          background-color: #fff;
        }
        p {
          a {
            color: #fff;
            text-decoration: none;
          }
        }
      }
    }
  }
</style>