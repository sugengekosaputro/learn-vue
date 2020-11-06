<template>
  <div class="home">
    <CustomerCard />
    <Appid />
    <DropdownList />
  </div>
</template>

<script>
// @ is an alias to /src
import CustomerCard from "@/components/CustomerCard.vue";
import Appid from "@/components/Appid.vue";
import DropdownList from "@/components/DropdownList.vue";

export default {
  name: "Home",
  components: {
    CustomerCard,
    Appid,
    DropdownList
  }
};
</script>

<style lang="scss">

</style>
