<template>
  <div class="card">
    <div class="customer-image">
      <img src alt srcset width="48px" height="48px" style="border-radius: 50%" />
    </div>

    <div class="customer-info">
      <span>Name</span>
      <span>Name</span>
      <span>Name</span>
    </div>

    <span class="customer-status">Lengkap/Belum</span>
  </div>
</template>

<script>
export default {
  name: "CustomerCard"
};
</script>

<style lang="scss">
.card {
  background-color: white;
  width: 100%;
  min-height: 120px;
  overflow: hidden;
  box-shadow: 1px 2px 7px 0 $grey-2;
  border-radius: 2px;
  padding: 16px;
  position: relative;

  .customer-image {
    position: absolute;
  }

  .customer-info {
    display: flex;
    flex-direction: column;
    text-align: start;
    padding-left: 90px;
  }

  .customer-status {
    position: absolute;
    right: 16px;
    background-color: $color-success;
    border-radius: 4px;
    color:white;
    padding: 2px;
  }
}
</style>