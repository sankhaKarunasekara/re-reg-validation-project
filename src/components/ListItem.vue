<template>
  <div
    class="bg-gray-100 px-8 py-4 flex items-center border-b border-gray-300 hover:bg-gray-200 cursor-pointer"
    @click="changeTheCheckBoxValue()"
  >
    <input
      type="checkbox"
      class="form-checkbox h-5 w-5 text-blue-600"
      v-model="checkboxValue"
    />
    <div class="flex ml-4">
      <img
        src="../assets/images/critical.png"
        class="w-10 h-10 object-cover rounded object-top"
      />
      <div class="flex flex-col pl-4">
        <h2 class="font-normal text-sm">{{ item.condition }}</h2>
        <h3 class="text-gray-700 text-sm">
          {{ sectionName }}
        </h3>
        <div
          class="uppercase text-xs text-gray-600 leading-tight font-semibold"
        >
          {{ tabName }}
        </div>
      </div>
    </div>
    <!-- <button
      class="text-gray-500 flex items-center text-sm focus:outline-none rounded ml-auto py-2 leading-none"
    >
      <svg
        stroke="currentColor"
        stroke-width="2"
        fill="none"
        stroke-linecap="round"
        stroke-linejoin="round"
        class="w-4 h-4 mr-2"
        viewBox="0 0 24 24"
      >
        <circle cx="12" cy="12" r="3" />
        <path
          d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 010 2.83 2 2 0 01-2.83 0l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-2 2 2 2 0 01-2-2v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83 0 2 2 0 010-2.83l.06-.06a1.65 1.65 0 00.33-1.82 1.65 1.65 0 00-1.51-1H3a2 2 0 01-2-2 2 2 0 012-2h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 010-2.83 2 2 0 012.83 0l.06.06a1.65 1.65 0 001.82.33H9a1.65 1.65 0 001-1.51V3a2 2 0 012-2 2 2 0 012 2v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 0 2 2 0 010 2.83l-.06.06a1.65 1.65 0 00-.33 1.82V9a1.65 1.65 0 001.51 1H21a2 2 0 012 2 2 2 0 01-2 2h-.09a1.65 1.65 0 00-1.51 1z"
        />
      </svg>
      Edit
    </button> -->
  </div>
</template>

<script>
export default {
  name: "ListItem",
  props: {
    item: {
      type: Object,
      default: () => {},
    },
    tabName: {
      type: String,
      default: "",
    },
    sectionName: {
      type: String,
      default: "",
    },
  },

  data() {
    return {
      checkboxValue: false,
    };
  },
  methods: {
    updateValue: function () {
      this.$emit("record-checkbox-value", {
        item: this.item,
        tabName: this.tabName,
        sectionName: this.sectionName,
        checkboxValue: this.checkboxValue,
      });
    },

    changeTheCheckBoxValue: function () {
      this.checkboxValue = !this.checkboxValue;
      this.updateValue();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
