<template>
  <Component :is="is" :to="to" :href="href" @click="onClick" class="item">
    <slot />
  </Component>
</template>

<script>
export default {
  name: "DropdownItem",

  inject: ["dropdown"],

  data() {
    return {};
  },
  props: {
    href: {
      type: String,
      default: undefined,
    },
    to: {
      type: [String, Object],
      default: undefined,
    },
  },
  methods: {
    onClick(evt) {
      this.$emit("click", evt);
      this.closeDropdown();
    },

    closeDropdown() {
      this.dropdown.close();
    },
  },
  computed: {
    is() {
      if (typeof this.to !== "undefined") {
        return "RouterLink";
      }
      if (typeof this.href !== "undefined") {
        return "a";
      }
      return "button";
    },
  },
};
</script>

<style scoped>
.item {
  display: block;
  padding: 0.7rem 1rem;
  cursor: pointer;
  width: 100%;
  display: flex;
  align-items: flex-start;
}

.item:hover {
  background-color: #f7f7f7;
  color: #262626;
}
</style>
