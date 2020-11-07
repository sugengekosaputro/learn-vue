<template>
  <div class="about">
    <div class="head">
      <!-- <DropdownList
        @on-item-selected="dropdownSelection = $event"
        @on-item-reset="dropdownSelection = {}"
        :msg="msg"
        class="sentra-search"
      /> -->
      <div class="cok" @click="modal = false"></div>
      <div class="sentra-search">
        <div class="dropdown">
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
        <span class="clear" @click="clear">x</span>
      </div>
      <button class="btn-search">Cari</button>
    </div>

    <div class="result">
      Hasil Pencarian hahaha
    </div>

    <hr />
  </div>
</template>

<script>
//import DropdownList from "@/components/DropdownList.vue";
import axios from "axios";
export default {
  data() {
    return {
      // dropdownSelection: {},
      modal: false,
      item: "",
      msg: false,
      items: [],
      filteredItems: [],
      apiUrl: "https://restcountries.eu/rest/v2/all?fields=name;flag"
    };
  },
  // components: {
  //   DropdownList
  // },
  methods: {
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
    clear() {
      this.item = "";
    }
  },
  mounted() {
    this.getData();
  },
  watch: {
    item() {
      this.filterItems();
    }
  }
};
</script>

<style lang="scss" scoped>
.cok {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0px;
  top: 0px;
  z-index: 1;
}

.sentra-search {
  position: relative;
}
.clear {
  position: absolute;
  z-index: 10;
  top: 7px;
  right: 15px;
  cursor: pointer;
}
.head {
  display: inline-flex;
  flex-direction: row;
  justify-content: flex-start;
}

.btn-search {
  width: 120px;
  height: 40px;
  border-radius: 8px;
  background-color: #f4831f;
  border: none;
  color: white;
  margin-left: 10px;
  z-index: 2;
}

.result {
  margin-top: 56px;
  text-align: start;
}

@media screen and (max-width: 600px) {
  #app {
    padding: 24px;
  }

  .head {
    display: flex;
    flex-direction: row;
  }
  .dropdown-input,
  .dropdown-selected {
    width: 168px;
  }

  .dropdown-input-text {
    max-width: 256px;
  }

  .sentra-search {
    width: 256px;
  }
  .btn-search {
    background-color: #f4831f;
  }

  .result {
    margin-top: 56px;
  }
}
</style>