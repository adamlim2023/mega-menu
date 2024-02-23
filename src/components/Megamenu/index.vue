<template>
  <div class="header">
    <Menu :menu-items="menuItems" :open="isOpen" />
    <button @click="handleToggleOpen" class="menu-button">
      <i class="fas fa-bars" v-if="!isOpen"></i>
      <i class="fas fa-close" v-else></i>
    </button>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Menu from "./Menu.vue";
const isOpen = ref(false);
const menuItems = [
  {
    key: "buy",
    icon: null,
    title: "Buy Crypto",
    description: null,
    badge: null,
    isViewLink: false,
    to: null,
    childrenColumns: 1,
    children: [
      {
        key: "quick",
        icon: "fas fa-plus",
        title: "Quick Buy",
        description: "Fast and accessible transactions",
        badge: null,
        isViewLink: true,
        to: "/buy/quick",
        childrenColumns: 0,
      },
      {
        key: "p2p",
        icon: "fas fa-user",
        title: "P2P Trading",
        description: "Myriads of merchants with better price",
        badge: null,
        isViewLink: true,
        to: "/buy/p2p",
        childrenColumns: 0,
      },
      {
        key: "bank",
        icon: "fas fa-wallet",
        title: "Bank Deposit",
        description: "Deposit via bank transfer or online payments",
        badge: "PROMO",
        isViewLink: true,
        to: "/buy/bank",
        childrenColumns: 0,
      },
    ],
  },
  {
    key: "markets",
    icon: null,
    title: "Markets",
    description: null,
    badge: null,
    isViewLink: false,
    to: "/markets",
    childrenColumns: 0,
  },
  {
    key: "spot",
    icon: null,
    title: "Spot",
    description: null,
    badge: null,
    isViewLink: false,
    to: null,
    childrenColumns: 1,
    children: [
      {
        key: "spot",
        icon: "fas fa-refresh",
        title: "Spot",
        description: "Trade hot assets in minutes",
        badge: null,
        isViewLink: true,
        to: "/trade/spot",
        childrenColumns: 0,
      },
      {
        key: "convert",
        icon: "fas fa-user",
        title: "Convert",
        description: "The easiest way to trade",
        badge: null,
        isViewLink: true,
        to: "/trade/convert",
        childrenColumns: 0,
      },
    ],
  },
  {
    key: "derivatives",
    icon: null,
    title: "Derivatives",
    description: null,
    badge: null,
    isViewLink: false,
    to: null,
    childrenColumns: 1,
    children: [
      {
        key: "perp",
        icon: "fas fa-clipboard",
        title: "Perpetual Futues",
        description: "Suitable for more experienced traders",
        badge: null,
        isViewLink: true,
        to: "/trade/prep",
        childrenColumns: 0,
      },
      {
        key: "mt5",
        icon: "fas fa-user",
        title: "MT5",
        description: "A specialized tool for professionals",
        badge: null,
        isViewLink: true,
        to: "/trade/mt5",
        childrenColumns: 1,
        children: [
          {
            key: "mt5-rules",
            icon: null,
            title: "MT5 Rules",
            description: "MT5 Rules",
            badge: null,
            isViewLink: true,
            to: "/rules/mt5",
            childrenColumns: 0,
          },
          {
            key: "mt5-guid",
            icon: null,
            title: "MT5 Guide",
            description: "MT5 Guide",
            badge: null,
            isViewLink: true,
            to: "/trade/mt5",
            childrenColumns: 0,
          },
        ],
      },
    ],
  },
  {
    key: "more",
    icon: null,
    title: "More",
    description: null,
    badge: null,
    isViewLink: false,
    to: null,
    childrenColumns: 3,
    children: [
      {
        key: "about",
        icon: "fas fa-refresh",
        title: "About",
        description: "About Us",
        badge: null,
        isViewLink: true,
        to: "/page/about",
        childrenColumns: 0,
      },
      {
        key: "contact",
        icon: "fas fa-envelope",
        title: "Contact Us",
        description: "Contact Us",
        badge: null,
        isViewLink: true,
        to: "/page/contact",
        childrenColumns: 0,
      },
      {
        key: "vip",
        icon: "fas fa-envelope",
        title: "VIP benefits",
        description: "VIP benefits",
        badge: null,
        isViewLink: true,
        to: "/page/vip",
        childrenColumns: 0,
      },
      {
        key: "academy",
        icon: "fas fa-envelope",
        title: "Academy",
        description: "Academy",
        badge: null,
        isViewLink: true,
        to: "/page/academy",
        childrenColumns: 0,
      },
      {
        key: "help",
        icon: "fas fa-envelope",
        title: "Help Center",
        description: "Help Center",
        badge: null,
        isViewLink: true,
        to: "/page/help",
        childrenColumns: 0,
      },
    ],
  },
];

const handleToggleOpen = () => {
  isOpen.value = !isOpen.value;
}
</script>

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css";
.header {
  width: 100%;
  height: 64px;
  position: relative;
  border-bottom: 1px solid #f4f5f6;
  background: #fff;
}

.menu-button {
  width: 32px;
  height: 32px;
  padding: 0;
  background: transparent;
  border: none;
  cursor: pointer;
  font-size: 16px;
  position: absolute;
  top: 50%;
  right: 20px;
  transform: translateY(-50%);
  display: none;
}

@media(max-width: 750px) {
  .menu-button {
    display: block;
  }
}

/* import fonts */

@font-face {
  font-family: "HarmonyOS Sans";
  font-weight: 900;
  src: url("../../assets/fonts/HarmonyOS_Sans_Black.woff2");
}

@font-face {
  font-family: "HarmonyOS Sans";
  font-weight: 700;
  src: url("../../assets/fonts/HarmonyOS_Sans_Bold.woff2");
}

@font-face {
  font-family: "HarmonyOS Sans";
  font-weight: 500;
  src: url("../../assets/fonts/HarmonyOS_Sans_Medium.woff2");
}

@font-face {
  font-family: "HarmonyOS Sans";
  font-weight: 400;
  src: url("../../assets/fonts/HarmonyOS_Sans_Regular.woff2");
}

@font-face {
  font-family: "HarmonyOS Sans";
  font-weight: 300;
  src: url("../../assets/fonts/HarmonyOS_Sans_Light.woff2");
}

@font-face {
  font-family: "HarmonyOS Sans";
  font-weight: 100;
  src: url("../../assets/fonts/HarmonyOS_Sans_Thin.woff2");
}
</style>
