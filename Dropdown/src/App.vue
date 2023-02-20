<template>
  <div id="app">
    <h3>Componente Dropdown</h3>

    <div class="drops">
      <DropDown title="Menu">
        <DropdownItem href="https://google.com">Item 1</DropdownItem>
        <DropdownItem>Item 2</DropdownItem>
        <DropdownItem>Item 3</DropdownItem>
        <DropdownDivider />
        <DropdownItem @click="onItem4Click">Item 4</DropdownItem>
        <DropdownItem>Item 5</DropdownItem>
        <DropdownDivider />
        <DropdownItem>Item 5</DropdownItem>
      </DropDown>
      <DropDown title="Menu" no-icon rounded naked>
        <DropdownItem href="https://google.com">Item 1</DropdownItem>
        <DropdownItem>Item 2</DropdownItem>
        <DropdownItem>Item 3</DropdownItem>
        <DropdownDivider />
        <DropdownItem @click="onItem4Click">Item 4</DropdownItem>
        <DropdownItem>Item 5</DropdownItem>
        <DropdownDivider />
        <DropdownItem>Item 5</DropdownItem>
      </DropDown>
    </div>
  </div>
</template>

<script>
import DropDown from "@/components/DropDown.vue";
import DropdownItem from "@/components/DropdownItem.vue";
import DropdownDivider from "@/components/DropdownDivider.vue";

export default {
  name: "App",
  components: {
    DropDown,
    DropdownItem,
    DropdownDivider,
  },
  methods: {
    onItem4Click(evt) {
      console.log("click item 4", evt);
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

h3 {
  margin-bottom: 2rem;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  text-align: center;
  color: #2c3e50;
  margin-top: 50px;
}

.drops {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
}
</style>
