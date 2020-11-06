<template>
  <div class="appid">
    <div class="appid-info">
      <span class="appid-code">Appid: { text }</span> &bull;
      <span class="appid-product">Name</span>
    </div>
    <div class="card">
      <div class="appid-documents">
        <Document type="ABC" />
        <Document type="ABC" />
        <Document type="ABC" />
        <Document type="ABC" />
        <Document type="ABC" />
        <Document type="ABC" />
        <Document type="ABC" />
        <Document type="ABC" />
      </div>

      <div class="document-footer">
        <button class="btn-search" />
      </div>
    </div>
  </div>
</template>

<script>
import Document from "@/components/Document.vue";

export default {
  name: "Appid",
  components: {
    Document
  }
};
</script>

<style lang="scss">
.appid {
  .appid-info {
    display: flex;
    align-content: flex-start;
    margin-bottom: 16px;
  }

  .appid-documents {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
}
</style>