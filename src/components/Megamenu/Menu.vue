<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "Menu",
  props: {
    menuItems: {
      type: Array,
      required: true,
    },
    isRoot: {
      type: Boolean,
      default: true,
    },
    columns: {
      type: Number,
      default: 1,
    },
  },
  setup() {},
});
</script>

<template>
  <ul
    :class="{ container: isRoot }"
    :style="{ 'grid-template-columns': 'auto '.repeat(columns).slice(0, -1) }"
  >
    <li v-for="item in menuItems" :key="item.key">
      <div>
        <i :class="item.icon" v-if="item.icon"></i>
        <div>
          <span>{{ item.title }}</span>
          <span v-if="item.description">{{ item.description }}</span>
        </div>
      </div>
      <Menu
        v-if="item.children"
        :menu-items="item.children"
        :isRoot="false"
        :columns="item.childrenColumns"
      />
    </li>
  </ul>
</template>

<style scoped>
@import "https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css";

.container * {
  box-sizing: border-box;
}

ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.container {
  width: 100%;
  height: 100%;
  display: flex;
  font-family: "HarmonyOs Sans";
  font-weight: 400;
  border-bottom: 1px solid #f4f5f6;
  background: #fff;
  margin: 0;
  display: flex;
  padding: 0;
}
.container > li {
  min-width: auto !important;
  display: flex;
  align-items: center;
  height: 100%;
  padding: 8px 12px !important;
  position: relative;
  border-radius: 0px !important;
}

.container > li:hover {
  background: #fff !important;
}

.container > li > div > div > span:first-child {
  font-size: 14px !important;
  color: #000 !important;
  font-weight: 400 !important;
}

.container > li > ul {
  top: auto !important;
  bottom: 0;
  left: 0;
  right: auto !important;
  transform: translateY(100%) !important;
}

.container > li > ul {
  display: grid !important;
  scale: 0;
}

.container > li:hover > ul {
  scale: 1;
}

.container > li ul {
  width: max-content;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.05) 0px 10px 20px 0px;
  top: 0;
  right: 0;
  transform: translateX(100%);
  display: none;
  gap: 12px;
  padding: 20px;
  background: #fff;
  transform-origin: bottom center;
  transition: 0.2s;
}


.container li:hover > ul {
  display: grid;
}

.container ul {
  position: absolute;
}

.container li {
  min-width: 260px;
  position: relative;
  cursor: pointer;
  padding: 8px;
  border-radius: 8px;
}

.container li:hover {
  background: #f4f5f6;
}

.container li > div {
  display: flex;
  align-items: center;
  gap: 15px;
}

.container li > div > div {
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.container li > div > div > span:first-child {
  font-size: 14px;
  font-weight: 500;
  color: #000;
}

.container li > div > div > span:last-child {
  font-size: 12px;
  color: rgba(0, 0, 0, 0.4);
}

.container > li::after {
  position: absolute;
  bottom: 0;
  left: 12px;
  right: 12px;
  height: 3px;
  background: #0047ff;
  content: "";
  display: none;
}

.container > li:hover::after {
  display: block;
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
