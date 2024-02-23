<script>
import { defineComponent, ref } from "vue";
import Menu from "./Menu.vue";

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
  setup() {
    const handleToggleOpen = (event, item) => {
      if (item.children) {
        const arrowElem = event.target.closest("li").firstChild.lastChild;
        const arrowStyle = window.getComputedStyle(arrowElem);
        const rotate = arrowStyle.rotate;
        arrowElem.setAttribute(
          "style",
          `rotate: ${rotate === "0deg" ? "180deg" : "0deg"}`
        );

        const listElem = event.target.closest("li").lastChild;
        const listStyle = window.getComputedStyle(listElem);
        const display = listStyle.display;
        listElem.setAttribute(
          "style",
          `display: ${
            display !== `none` ? `none !important` : `grid !important`
          }`
        );
      }
    };

    return { handleToggleOpen };
  },
});
</script>

<template>
  <ul
    :class="{ container: isRoot }"
    :style="{ 'grid-template-columns': 'auto '.repeat(columns).slice(0, -1) }"
  >
    <li v-for="item in menuItems" :key="item.key">
      <div @click="(e) => handleToggleOpen(e, item)">
        <i :class="item.icon" v-if="item.icon"></i>
        <div>
          <span>{{ item.title }}</span>
          <span v-if="item.description">{{ item.description }}</span>
        </div>
        <i class="fas fa-angle-down arrow" v-if="item.children"></i>
      </div>
      <template v-if="item.children">
        <Menu
          :menu-items="item.children"
          :isRoot="false"
          :columns="item.childrenColumns"
        />
      </template>
    </li>
  </ul>
</template>

<style scoped>
.container * {
  box-sizing: border-box;
}

ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

.arrow {
  position: absolute;
  right: 20px;
  top: 12px;
  display: none;
  transition: 0.1s !important;
  rotate: 0deg;
}

[dir="rtl"] .arrow {
  left: 20px;
  right: auto !important;
}

@media screen and (orientation: landscape) and (min-width: 751px) {
  .container li:hover > ul {
    display: grid !important;
    scale: 1;
  }

  .container li:hover > div .arrow {
    rotate: 180deg;
  }
}

@media screen and (orientation: portrait) and (max-width: 750px) {
  .container {
    height: calc(100vh - 200px) !important;
  }
}

@media screen and (orientation: landscape) and (max-width: 750px) {
  .container {
    height: calc(100vh - 120px) !important;
  }
  .container li ul {
    transform: none !important;
  }
}

[dir="rtl"] .container > li ul {
  left: 0 !important;
  transform: translateX(-100%);
  right: auto !important;
}

[dir="rtl"] .container > li > ul {
  right: 0px !important;
}

.container {
  width: 100%;
  display: flex;
  font-family: "HarmonyOs Sans";
  font-weight: 400;
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
}

@media screen and (min-width: 751px) {
  .container {
    display: flex !important;
    height: 100%;
  }

  .container > li > ul {
    transform: translate(0, 100%) !important;
  }

  .container > li ul {
    transform: translate(100%, 0);
  }

  .container li:hover {
    background: #f4f5f6;
  }

  .container > li:hover {
    background: #fff !important;
  }
}

.container > li ul {
  scale: 0;
}

.container > li ul {
  width: max-content;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.05) 0px 10px 20px 0px;
  top: 0;
  right: 0;
  gap: 12px;
  padding: 20px;
  background: #fff;
  transform-origin: bottom center;
  transition-property: all;
  transition: 0.2s all;
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

@media screen and (max-width: 750px) {
  .arrow {
    display: inline;
  }

  .container {
    position: fixed;
    top: 65px;
    right: 0;
    left: 0;
    flex-direction: column;
    overflow-y: scroll;
    padding: 10px 0;
  }

  .container > li > ul {
    transform: none !important;
  }

  .container ul {
    width: 100% !important;
    position: relative;
    scale: 1 !important;
    display: none;
    top: auto !important;
    right: auto !important;
    bottom: auto !important;
    left: auto !important;
    transform: none !important;
    box-shadow: none !important;
    padding: 0 !important;
    gap: 0 !important;
    grid-template-columns: auto !important;
  }

  .container > li::after {
    display: none !important;
  }

  .container li {
    flex-direction: column;
    align-items: flex-start;
    padding: 0 !important;
    height: auto !important;
    border-radius: 0 !important;
  }

  .container li > div {
    gap: 22px !important;
  }

  .container li > div > div > span:first-child {
    font-size: 16px !important;
    font-weight: 400 !important;
  }

  .container > li > div {
    width: 100%;
    padding: 0 20px;
    min-height: 40px;
  }
  .container li > div {
    padding: 8px 20px;
  }
}
</style>
