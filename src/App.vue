<template>
  <div id="app" class="bg-grey-100">
    <div
      class="
        h-screen
        w-screen
        bg-indigo-400
        overflow-hidden
        absolute
        flex
        items-center
      "
    >
      <div
        class="
          w-screen
          h-64
          absolute
          top-0
          opacity-50
          left-0
          -my-40
          -mx-64
          bg-indigo-300
          rounded-full
        "
      ></div>
      <div class="w-64 h-64 -mx-32 bg-indigo-300 opacity-50 rounded-full"></div>
      <div
        class="
          w-64
          h-64
          ml-auto
          relative
          opacity-50
          -mr-32
          bg-indigo-300
          rounded-full
        "
      ></div>
      <div
        class="
          w-screen
          h-64
          absolute
          opacity-50
          bottom-0
          right-0
          -my-40
          -mx-64
          bg-indigo-300
          rounded-full
        "
      ></div>
    </div>

    <div class="container mx-auto h-screen pt-16 pb-16 px-8 relative">
      <!-- TODO: add a heading here-->
      <div
        class="
          flex
          w-full
          rounded-lg
          h-full
          lg:overflow-hidden
          overflow-auto
          lg:flex-row
          flex-col
          shadow-2xl
        "
      >
        <div class="lg:w-1/2 bg-white text-gray-800 flex flex-col">
          <div class="p-8 shadow-md relative bg-white">
            <!-- <div class="flex items-center">
              <img
                src="https://randomuser.me/api/portraits/men/1.jpg"
                class="w-10 h-10 block rounded object-cover object-top"
              />
              <div class="text-indigo-600 font-medium ml-3">
                Holden Caulfield
              </div>
              <button
                class="bg-indigo-100 text-indigo-400 ml-auto w-8 h-8 flex items-center justify-center rounded"
              >
                <svg
                  stroke="currentColor"
                  class="w-4 h-4"
                  viewBox="0 0 24 24"
                  stroke-width="2.2"
                  fill="none"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path
                    d="M18 8A6 6 0 006 8c0 7-3 9-3 9h18s-3-2-3-9M13.73 21a2 2 0 01-3.46 0"
                  />
                </svg>
              </button>
            </div> -->
            <div class="flex">
              <div class="mr-auto">
                <h1 class="font-medium text-lg mt-6">
                  Re Registration Issues List
                </h1>
                <p class="text-gray-600 text-sm">
                  search and find a issue and click the check box.
                  <a
                    href="#"
                    class="text-blue-800 font-semibold"
                    @click="openIssuesExcel()"
                  >
                    click here to add a new issue.</a
                  >
                </p>
              </div>
            </div>
            <div class="mt-6 flex">
              <div class="relative ml-auto flex-1 sm:block hidden">
                <input
                  placeholder="Search"
                  type="text"
                  ref="search"
                  v-model="search"
                  class="
                    w-full
                    border
                    rounded
                    border-gray-400
                    h-full
                    focus:outline-none
                    pl-4
                    pr-8
                    text-gray-700 text-sm text-gray-500
                  "
                />
                <svg
                  stroke="currentColor"
                  class="w-4 h-4 absolute right-0 top-0 mt-3 mr-2 text-gray-500"
                  stroke-width="2"
                  fill="none"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  viewBox="0 0 24 24"
                >
                  <circle cx="11" cy="11" r="8" />
                  <path d="M21 21l-4.35-4.35" />
                </svg>
              </div>
              <button
                class="
                  bg-indigo-500
                  ml-8
                  sm:block
                  hidden
                  text-white
                  py-2
                  text-sm
                  px-3
                  rounded
                  focus:outline-none
                  bg-indigo-300
                  cursor-pointer
                "
                @click="clearSearch()"
              >
                Clear Search
              </button>
            </div>
          </div>
          <div class="overflow-auto flex-grow">
            <div v-for="(item, index) in validationQuestions" :key="index">
              <ListItem
                v-if="isSearch(item, item.tab, item.section)"
                :tab-name="item.tab"
                :section-name="item.section"
                :item="item"
                @record-checkbox-value="recordCheckboxValue"
                :key="componentKey"
              />
            </div>
          </div>
        </div>
        <div class="lg:w-1/2 bg-indigo-600 text-white flex flex-col">
          <div class="p-8 bg-indigo-700 flex items-center">
            <!-- <img
              src="https://pbs.twimg.com/profile_images/1000050491970260993/FJkauyEa.jpg"
              class="w-16 h-16 mr-4 object-top object-cover rounded"
            /> -->
            <div class="mr-auto">
              <h1 class="text-xl leading-none mb-1">Generated Email</h1>
              <h2 class="text-indigo-400 text-sm">
                you can copy and paste it in the email body
              </h2>
            </div>
            <button
              @click="clearAll()"
              class="
                bg-indigo-600
                text-white
                py-2
                text-sm
                px-3
                rounded
                focus:outline-none
                hover:bg-indigo-400
                shadow
                cursor-pointer
              "
            >
              Clear All
            </button>
          </div>
          <div class="p-8 flex flex-1 items-start overflow-auto">
            <div class="flex-1 h-full">
              <div
                class="
                  h-full
                  w-full
                  bg-transparent
                  text-black
                  mt-2
                  justify-between
                "
              >
                <!-- <vue-editor
                  style="width: 100%; height: 100%; box-sizing: border-box"
                  placeholder="Message..."
                  class="w-full p-2 focus:outline-none focus:ring focus:border-blue-300 border-blue-100 border shadow resize-none text-base rounded-sm box-border bg-white"
                  v-model="mailtextbox"
                ></vue-editor> -->
                <textarea
                  v-model="mailtextbox"
                  style="width: 100%; height: 100%; box-sizing: border-box"
                  placeholder="Message..."
                  class="
                    w-full
                    p-2
                    focus:outline-none focus:ring focus:border-blue-300
                    border-blue-100 border
                    shadow
                    resize-none
                    text-base
                    rounded-sm
                    box-border
                    bg-white
                  "
                ></textarea>
              </div>
            </div>
          </div>
          <button
            @click="copy(mailtextbox)"
            class="
              bg-indigo-600
              m-1
              text-white
              font-semibold
              py-2
              text-sm
              px-3
              rounded
              shadow
              focus:outline-none
              hover:bg-indigo-500
              shadow
              cursor-pointer
            "
          >
            Copy
          </button>
        </div>
      </div>
    </div>

    <div class="fixed h-screen right-0 top-0 items-center flex">
      <div
        class="
          p-2
          bg-white
          border-l-4 border-t-4 border-b-4 border-indigo-400
          inline-flex
          items-center
          rounded-tl-lg
          shadow-2xl
          rounded-bl-lg
          z-10
          flex-col
        "
      >
        <button
          class="
            bg-gray-500
            w-5
            h-5
            rounded-full
            mb-2
            outline-none
            focus:outline-none
          "
          theme-button="gray"
        ></button>
        <button
          class="
            bg-red-500
            w-5
            h-5
            rounded-full
            mb-2
            outline-none
            focus:outline-none
          "
          theme-button="red"
        ></button>
        <button
          class="
            bg-green-500
            w-5
            h-5
            rounded-full
            mb-2
            outline-none
            focus:outline-none
          "
          theme-button="green"
        ></button>
        <button
          class="
            bg-blue-500
            w-5
            h-5
            rounded-full
            mb-2
            outline-none
            focus:outline-none
          "
          theme-button="blue"
        ></button>
        <button
          class="
            bg-indigo-500
            w-5
            h-5
            rounded-full
            mb-2
            outline-none
            focus:outline-none
          "
          theme-button="indigo"
        ></button>
        <button
          class="
            bg-purple-500
            w-5
            h-5
            rounded-full
            mb-2
            outline-none
            focus:outline-none
          "
          theme-button="purple"
        ></button>
        <button
          class="
            bg-pink-500
            w-5
            h-5
            rounded-full
            outline-none
            focus:outline-none
          "
          theme-button="pink"
        ></button>
      </div>
    </div>
  </div>
</template>

<script>
import ListItem from "./components/ListItem.vue";
// import validationQuestions from "@/data/validation.json";
import axios from "axios";
// import { VueEditor } from "vue2-editor";

// var gsheet_url =
//   "https://spreadsheets.google.com/feeds/list/1eNmGC4mZpIGx9vyL_Y0m0wEvsnlREGYoj04LH9atoTg/1/public/values?alt=json";
let gsheet_url =
  "https://docs.google.com/spreadsheets/d/10MKW1D4HVBARRYZMzgksxZ66uZxEG3fvS3L20GyZagc/gviz/tq?tqx=out:json";

export default {
  name: "App",

  components: {
    ListItem,
    // VueEditor,
  },

  async mounted() {
    const allElements = document.querySelectorAll(
      '*:not([theme-button]):not([class*="gray"])'
    );
    const themeButtons = document.querySelectorAll("[theme-button]");
    const escapeRegExp = (string) =>
      string.replace(/[.*+?^${}()|[\]\\]/g, "\\$&");
    const replaceAll = (str, term, replacement) =>
      str.replace(new RegExp(escapeRegExp(term), "g"), replacement);
    let currTheme = "indigo";

    const changeTheme = (theme) => {
      allElements.forEach((element) => {
        if (element.getAttribute("class") !== null) {
          const newClasses = replaceAll(
            element.getAttribute("class"),
            currTheme,
            theme
          );
          element.setAttribute("class", newClasses);
        }
      });
      currTheme = theme;
    };

    themeButtons.forEach((button) => {
      button.addEventListener("click", (e) => {
        changeTheme(e.target.getAttribute("theme-button"));
      });
    });

    try {
      const response = await axios.get(gsheet_url);

      const r = response.data.match(
        /google\.visualization\.Query\.setResponse\(([\s\S\w]+)\)/
      );
      const self = this;
      if (r && r.length == 2) {
        const obj = JSON.parse(r[1]);
        const table = obj.table;
        const header = table.cols.map(({ label }) => label);
        const rows = table.rows.map(({ c }) =>
          c.map((e) => (e ? e.v || "" : ""))
        ); // Modified from const rows = table.rows.map(({c}) => c.map(({v}) => v));

        console.table(header);
        console.table(rows);

        rows.forEach(function (value) {
          let entry = {
            timestamp: value[0],
            tab: value[1],
            section: value[2],
            issue: value[3],
            type: value[4],
            message: value[5],
          };
          self.validationQuestions.push(entry);
        });
      }
    } catch (e) {
      alert(e);
    }
  },

  data() {
    return {
      validationQuestions: [],
      checkedItemsList: [],
      googleQuestions: [],
      mailtextbox: "",
      search: "",
      componentKey: 0,
    };
  },

  methods: {
    recordCheckboxValue: function ({
      item,
      tabName,
      sectionName,
      checkboxValue,
    }) {
      if (checkboxValue) {
        this.checkedItemsList.push({ tabName, sectionName, ...item });
      } else {
        this.checkedItemsList = this.checkedItemsList.filter(
          (checkedItem) =>
            !this.isTheSameItem(checkedItem, item, tabName, sectionName)
        );
      }
      this.mailtextbox = "";
      this.generateListItemsString();
    },

    generateListItemsString: function () {
      let i = 0;

      const listItems = this.checkedItemsList.filter(
        (item) =>
          !(
            (item.tabName == "Email" && item.sectionName == "Ending") ||
            (item.tabName == "Email" && item.sectionName == "Start")
          )
      );

      //Starts
      const starts = this.checkedItemsList.filter(
        (item) => item.tabName == "Email" && item.sectionName == "Start"
      );

      if (starts.length != 0) {
        for (i = 0; i < starts.length; i++) {
          this.mailtextbox = this.mailtextbox.concat(
            this.generateAListItem(i, starts[i])
          );
        }
      }

      //List Items
      for (i = 0; i < listItems.length; i++) {
        this.mailtextbox = this.mailtextbox.concat(
          this.generateAListItem(i, listItems[i])
        );
      }

      //Endings
      const endings = this.checkedItemsList.filter(
        (item) => item.tabName == "Email" && item.sectionName == "Ending"
      );

      if (endings.length != 0) {
        this.mailtextbox = this.mailtextbox.concat(endings[0].message);
      }
    },

    isTheSameItem(item1, item2, tabName, sectionName) {
      if (
        item1.issue == item2.issue &&
        item1.tabName == tabName &&
        item1.sectionName == sectionName
      ) {
        return true;
      } else {
        return false;
      }
    },

    generateAListItem(i, item) {
      let text = "";

      if (item.tab == "Email") {
        text = `${item.message}\n`;
      } else {
        text = `${i + 1}. ${item.message}\n\n`;
      }

      return text;
    },

    isSearch(item, tabName, sectionName) {
      return item.message
        .concat(` ${tabName} ${sectionName}`)
        .toLowerCase()
        .includes(this.search.toLowerCase());
    },

    clearAll: function () {
      this.search = "";
      this.mailtextbox = "";
      this.checkedItemsList = [];
      this.forceRerender();
    },

    clearSearch() {
      this.search = "";
      this.$refs.search.focus();
    },

    forceRerender() {
      this.componentKey += 1;
    },

    openIssuesExcel() {
      window.open(
        "https://docs.google.com/forms/u/0/d/e/1FAIpQLSdp1PvOefsd0v5l7A9O19LqcgK8vA_rnmQjd30ymSDEnBNhVw/formResponse",
        "_blank"
      );
    },

    async copy(s) {
      await navigator.clipboard.writeText(s);
    },
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
