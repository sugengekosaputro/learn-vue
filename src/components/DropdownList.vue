<template>
  <div class="dropdown">
    <!-- <input
      v-if="Object.keys(selectedItem).length === 0"
      ref="dropdowninput"
      v-model.trim="inputValue"
      class="dropdown-input"
      type="text"
      placeholder="Find country"
      v-on:focus.native="onFocus"
    />
    <div v-else @click="resetSelection" class="dropdown-selected">
      {{ selectedItem.name }}
    </div>
    <div v-show="(inputValue && apiLoaded) || previewed" class="dropdown-list">
      <div
        @click="selectItem(item)"
        v-show="itemVisible(item)"
        v-for="item in itemList"
        :key="item.name"
        class="dropdown-item"
      >
        {{ item.name }}
      </div>
    </div> -->

    <input
      type="text"
      autocomplete="off"
      class="dropdown-input"
      v-model="item"
      @input="filterItems"
      @focus="modal = true"
    />
    <div v-if="filteredItems && modal" class="dropdown-list">
      <div
        v-for="filtered in filteredItems"
        :key="filtered.name"
        @click="setItem(filtered)"
        class="dropdown-item"
      >
        {{ filtered.name }}
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: {
    msg: Boolean
  },
  data() {
    return {
      selectedItem: {},
      // inputValue: "",
      // itemList: [],
      // apiLoaded: false,
      // previewed: false,
      // apiUrl: "https://restcountries.eu/rest/v2/all?fields=name;flag"
      modal: this.msg,
      item: "",
      items: [],
      filteredItems: [],
      apiUrl: "https://restcountries.eu/rest/v2/all?fields=name;flag"
    };
  },
  mounted() {
    //    this.getList();
    this.getData();
    this.ping();
  },
  methods: {
    // resetSelection() {
    //   this.selectedItem = {};
    //   this.$nextTick(() => this.$refs.dropdowninput.focus());
    //   this.$emit("on-item-reset");
    // },
    // selectItem(theItem) {
    //   this.selectedItem = theItem;
    //   this.inputValue = "";
    //   this.$emit("on-item-selected", theItem);
    // },
    // itemVisible(item) {
    //   let currentName = item.name.toLowerCase();
    //   let currentInput = this.inputValue.toLowerCase();
    //   return currentName.includes(currentInput);
    // },
    // getList() {
    //   axios.get(this.apiUrl).then(response => {
    //     this.itemList = response.data;
    //     this.apiLoaded = true;
    //     console.log(response);
    //   });
    // },
    // preview(){
    //   if(!this.previewed) {
    //     this.previewed = true;
    //   }
    // }
    getData() {
      axios.get(this.apiUrl).then(response => {
        this.items = response.data;

        if (this.item.length === 0) {
          this.filteredItems = this.items;
        }
        console.log(this.filteredItems, "filter");
        console.log(this.items, "items");
      });
    },
    filterItems() {
      this.filteredItems = this.items.filter(item => {
        return item.name.toLowerCase().startsWith(this.item.toLowerCase());
      });
    },

    setItem(obj) {
      this.item = obj.name;
      this.modal = false;
      console.log("clicked");
    },
    close() {
      this.modal = false;
    },
    ping() {
      console.log(this.modal,"aaa");
    }
  },
  watch: {
    msg() {
      console.log("change wathc ","aaa");
    }
  }
};
</script>

<style>

.dropdown {
  position: relative;
  width: 100%;
  height: 100%;
  max-height: 40px;
  max-width: 658px;
  z-index: 10;
}
.dropdown-input-text {
  width: 68px;
  height: 40px;
  padding: 10px 16px;
  border: 1px solid transparent;
  background: #edf2f7;
  line-height: 1.5em;
  outline: none;
  border-radius: 8px;
}
.dropdown-input,
.dropdown-selected {
  width: 268px;
  height: 40px;
  padding: 10px 16px;
  border: 1px solid transparent;
  background: #edf2f7;
  line-height: 1.5em;
  outline: none;
  border-radius: 8px;
}
.dropdown-input:focus,
.dropdown-selected:hover {
  background: #fff;
  border-color: #e2e8f0;
}
.dropdown-input::placeholder {
  opacity: 0.7;
}
.dropdown-selected {
  cursor: pointer;
}
.dropdown-list {
  position: absolute;
  width: 100%;
  max-height: 200px;
  margin-top: 4px;
  overflow-y: auto;
  background: #ffffff;
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1),
    0 4px 6px -2px rgba(0, 0, 0, 0.05);
  border-radius: 8px;
}
.dropdown-item {
  display: flex;
  width: 100%;
  padding: 11px 16px;
  cursor: pointer;
}
.dropdown-item:hover {
  background: #edf2f7;
}
.dropdown-item-flag {
  max-width: 24px;
  max-height: 18px;
  margin: auto 12px auto 0px;
}

@media screen and (max-width: 600px) {
  .dropdown-input,
  .dropdown-selected {
    max-width: 168px;
  }

  .dropdown-input-text {
    max-width: 256px;
  }
}
</style>