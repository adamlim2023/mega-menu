<script>
import { defineComponent, reactive } from "vue";
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
    open: {
      type: Boolean,
      default: false,
    },
  },
  setup() {
    const state = reactive({
      isOpen: false
    });
    const handleToggleOpen = (item) => {
      if (item.children) {
        state.isOpen = !state.isOpen
      }
    };

    return { state, handleToggleOpen };
  },
});
</script>

<template>
  <ul
    :class="{ container: isRoot }"
    :style="{ 'grid-template-columns': 'auto '.repeat(columns).slice(0, -1) }"
    v-if="open"
  >
    <li v-for="item in menuItems" :key="item.key">
      <div @click="() => handleToggleOpen(item)">
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
        :open="state.isOpen"
      />
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

.container {
  width: 100%;
  height: 100%;
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
}

@media (min-width: 750px) {
  .container > li > ul {
    transform: translateY(100%) !important;
  }
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

@media (max-width: 750px) {
  .container {
    position: fixed;
    top: 65px;
    height: calc(100vh - 65px);
    right: 0;
    left: 0;
    flex-direction: column;
    overflow-y: scroll;
    padding: 10px 0;
  }

  .container ul {
    width: 100% !important;
    position: relative;
    scale: 1 !important;
    display: grid !important;
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
