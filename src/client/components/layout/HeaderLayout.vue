<template>
<div id="header" :style="{marginTop: this.alertsHeight}" :ref="'header'">
  <!--<img src="public/WebDollar-logo-black.png" id="logo"/>-->

  <div class="topnav" id="menu">

    <router-link to="/#mainSection" id="logoBox" class="active logoMenu" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <img v-on:click="this.collapseMenuBack" src="/public/assets/images/WebDollar-logo-white.png" alt="Cryptocurrency of the future" id="logo" title="Cryptocurrency of the future" />
    </router-link>

    <!---link to="/#papers" :class="mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">Paper</div>
    </router-link>-->

    <!--<a href="https://webdollarforum.com" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' " rel="noopener" target="_blank">
      <div v-on:click="this.collapseMenuBack">Forum</div>
    </a>-->

    <!--<router-link to="/faq" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">FAQ</div>
    </router-link>-->

    <!--<router-link to="/#team" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">Team</div>
    </router-link>-->
    
    <a href="https://t.me/LOFTpool" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' " rel="noopener" target="_blank">
      <div v-on:click="this.collapseMenuBack">Chat</div>
    </a>

    <a href="http://webdpools.com/LOFT/" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' " target="_blank" >
        <div v-on:click="this.collapseMenuBack">Statistic</div>
    </a>

    <router-link to="/#what-is-WebDollar" :class="mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">About</div>
    </router-link>

    <a href="https://www.webdscan.io/" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' " rel="noopener" target="_blank">
      <!--<router-link to="/explorer" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">-->
      <div v-on:click="this.collapseMenuBack">Explorer</div>
      <!--</router-link>-->
    </a>

    <router-link to="/bounties" :class="mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">Bounties</div>
    </router-link>

    <router-link to="/pool" :class="mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">Referral</div>
    </router-link>

    <a href="https://academy.webdollar.io" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' " rel="noopener" target="_blank">
      <div v-on:click="this.collapseMenuBack">Academy</div>
    </a>

    <router-link to="/partners/businesses" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">Partners</div>
    </router-link>

    <router-link to="/partners/exchanges" :class="this.mobileMenuOpened && this.isMobile ? 'openedMenuLink' : '' ">
      <div v-on:click="this.collapseMenuBack">Exchange</div>
    </router-link>

    <a href="javascript:void(0);" style="font-size:15px;" :style="{display: (mobileMenuOpened || isMobile==false) ? 'none':'block'}" class="icon showMenu" @click="this.showMobileMenu" :class="mobileMenuOpened ? 'openedMenuLink' : '' ">&#9776;</a>

  </div>
  <div id="WebDollarAlertsStickyBar"></div>

  <vue-cookie-accept-decline
          :ref="'poolCookieConsent'"
          :elementId="'poolCookieConsent'"
          :debug="false"
          :position="'top-left'"
          :type="'bar'"
          :disableDecline="false"
          :transitionName="'slideFromBottom'"
          @status="cookieStatus"
          @clicked-accept="cookieClickedAccept"
          @clicked-decline="cookieClickedDecline">

      <div slot="message">
          WARNING! Due to recent changes in the WebDollar Usage Policy we are required to inform you that WebDollar Team is not responsible of any losses you may experience from using a wallet interface hosted on third party websites, using the pool you accept all possible risks related to experimental software usage.Pool owner can't compensate any irreversible losses, but will do the best to prevent worst case.
      </div>

      <div slot="declineContent">
          NO, I DO NOT AGREE!
      </div>

      <div slot="acceptContent">
          YES, I UNDERSTAND!
      </div>
  </vue-cookie-accept-decline>
 </div>
</template>

<script>
import VueCookieAcceptDecline from 'vue-cookie-accept-decline';
import 'vue-cookie-accept-decline/dist/vue-cookie-accept-decline.css'
export default {

  name: "HeaderLayout",

  components: {
    VueCookieAcceptDecline
  },

  data() {
    return {
      screenWidth: 0,
      alertsHeight: 0,
      mobileMenuOpened: false,
      isMobile: false,
      alerts: [{
        message: 'test text'
      }, {
        message: 'test text 2'
      }]
    }
  },

  methods: {

    collapseMenuBack() {
      this.$refs['header'].style.zIndex = 10;
      this.mobileMenuOpened = false;
    },

    showMobileMenu() {
      this.$refs['header'].style.zIndex = 20;
      this.mobileMenuOpened = true;

    },

    verifyIfIsMobile() {

      if (this.screenWidth < 768) {

        this.isMobile = true;

      } else {

        this.isMobile = false;

      }

    },

cookieStatus (status) {
       this.status = status;
    },
cookieClickedAccept () {
       this.status = 'accept';

       window.location.href = "https://pool.maison/";
    },
cookieClickedDecline () {
       this.status = 'decline';
       window.location.href = "https://google.com/";
    },
cookieRemovedCookie () {
       this.status = null;
       this.$refs.poolCookieConsent.init();
    },
    
    addEvent(object, type, callback) {
      if (object === null || typeof(object) === 'undefined') return;
      if (object.addEventListener) {
        object.addEventListener(type, callback, false);
      } else if (object.attachEvent) {
        object.attachEvent("on" + type, callback);
      } else {
        object["on" + type] = callback;
      }
    }

  },

  mounted() {

    if (typeof window === 'undefined') return;

    this.addEvent(window, "resize", (event) => {

      this.screenWidth = window.innerWidth;
      this.verifyIfIsMobile();

    });

    this.addEvent(window, "scroll", (event) => {

      if (this.mobileMenuOpened == true) {
        this.collapseMenuBack();
      }

    });

    this.screenWidth = window.innerWidth;
    this.verifyIfIsMobile();

  }

}

</script>

<style type="text/css">
    .cookie__bar__buttons__button--decline {
	display:none !important;
    }
</style>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .cookie__bar__content div { margin-bottom: 10px; }
    
    div.cookie__bar {
	flex-direction: column;
    }
    .cookie__bar__content div {
        color: black;
    }
    /*h1,
    h2 {
        font-weight: normal;
    }
    ul {
        list-style-type: none;
        padding: 0;
    }
    li {
        display: inline-block;
        margin: 0 10px;
    }
    a {
        color: #42b983;
    }*/
</style>
