<template>
  <div class="about" @click="modal = false">
    <div class="head">
      <DropdownList
        @on-item-selected="dropdownSelection = $event"
        @on-item-reset="dropdownSelection = {}"
        class="sentra-search"
      />
      <button class="btn-search">Cari</button>
    </div>

    <div class="result">
      Hasil Pencarian hahaha
    </div>

    <hr />
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
  </div>
</template>

<script>
import DropdownList from "@/components/DropdownList.vue";
import axios from "axios";
export default {
  data() {
    return {
      dropdownSelection: {},
      modal: false,
      item: "",
      items: [],
      filteredItems: [],
      apiUrl: "https://restcountries.eu/rest/v2/all?fields=name;flag"
    };
  },
  components: {
    DropdownList
  },
  methods: {
    getData() {
      axios.get(this.apiUrl).then(response => {
        this.items = response.data;

      if (this.item.length === 0) {
        this.filteredItems = this.items
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
            console.log('clicked');
    },
    close(){
      this.modal = false;
    }
  },
  mounted() {
    this.getData();
  }
};
</script>

<style lang="scss" scoped>
.about {
  z-index: 0;
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