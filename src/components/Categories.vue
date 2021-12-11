<template>
  <div>
    <div v-if="isCateSet" @click="selectCategory(undefined)">remove filter</div>
    <div>
      <ul>
        <!-- remember to use :key -->
        <li
          v-for="category in categories"
          :key="category"
          @click="selectCategory(category)"
          :class="{selected: category == isCateSet}"
        >
          {{ category }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  //carefull to have this as a string
  props: ["categories"],
  data: () => {
    return {
      isCateSet: undefined,
    };
  },
  methods: {
    selectCategory(category) {
      this.isCateSet = category;
      this.$emit("setCategory", category);
    },
  },
};
</script>

<style scoped>
.selected {
  font-weight: bold;
}
</style>