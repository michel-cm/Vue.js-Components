<template>
  <div class="container">
    <button
      class="button-dropdown"
      @click.stop.prevent="toggle"
      :class="{ rounded: rounded, naked: !naked }"
    >
      {{ title }}
      <svg
        v-if="!noIcon"
        class="iconArrowDown"
        fill="currentColor"
        viewBox="0 0 20 20"
      >
        <path
          fill-rule="evenodd"
          d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
          clip-rule="evenodd"
        />
      </svg>
    </button>

    <div class="area-dropdown" v-show="isOpen">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: "DropDown",
  data() {
    return {
      isOpen: false,
    };
  },

  props: {
    title: {
      type: String,
      default: "Dropdown",
    },

    noIcon: {
      type: Boolean,
      default: false,
    },

    rounded: {
      type: Boolean,
      default: false,
    },

    naked: {
      type: Boolean,
      default: false,
    },
  },

  watch: {
    isOpen(value) {
      if (value) {
        this.$root.$emit("dropdown::open", this);
      }
    },
  },

  created() {
    this.$root.$on("dropdown::open", this.rootCloseListener);
  },

  mounted() {
    document.addEventListener("click", this.clickOutListener);
  },

  beforeDestroy() {
    document.removeEventListener("click", this.clickOutListener);
  },

  provide() {
    return {
      dropdown: this,
    };
  },

  methods: {
    toggle() {
      this.isOpen = !this.isOpen;
    },
    close() {
      this.isOpen = false;
    },
    clickOutListener(event) {
      if (!this.$el.contains(event.target)) {
        this.close();
      }
    },
    rootCloseListener(vm) {
      if (vm !== this) {
        this.close();
      }
    },
  },
};
</script>

<style scoped>
a {
  text-decoration: none;
  list-style: none;
  color: #262626;
}

button {
  background: none;
  outline: none;
  border: none;
  font-size: 1rem;
}

.button-dropdown {
  outline: 0;

  background-color: white;
  padding: 0.5rem 1rem;
  font-weight: bold;
  cursor: pointer;

  display: flex;
  align-items: center;
}

.rounded {
  border-radius: 4px;
}

.naked {
  border: 1px solid #ccc;
}

.iconArrowDown {
  width: 20px;
  height: 20px;
  margin-left: 0.3rem;
}

.container {
  display: inline-block;
  position: relative;
  text-align: left;
}

.area-dropdown {
  position: absolute;
  top: 0;
  right: 0;
  margin-top: 2.75rem;
  width: 256px;
  border-radius: 8px;
  border: 1px solid #ccc;
  padding: 0.5rem 0;
}
</style>
