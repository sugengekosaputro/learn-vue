<template>
  <div class="document">
    {{ type }}
    <div class="document-frame">
      
      <span class="label-grey">Seret dan Letakkan gambar atau</span>
      <button class="btn-outline">Ambil Gambar</button>
    </div>
    <div class="document-edit">
      Ubah Gambar | Lihat Gambar
    </div>
  </div>
</template>

<script>
export default {
  name: "Document",
  props: {
    type: String
  }
};
</script>

<style scoped lang="scss">
.document {
  margin: 6px;
  text-align: start;

  .document-frame {
    background-color: white;
    border: 1px solid $grey-2;
    border-radius: 8px;
    width: 247px;
    height: 158px;
    text-align: center;
    position: relative;
    overflow: hidden;

    .label-grey {
      position: relative;
      top: 75px;
      font-size: 12px;
      }

    .btn-outline {
      width: 144px;
      height: 32px;
      border-radius: 6px;
      border: 1px solid $color-secondary;
      color: $color-secondary;
      font-size: 14px;
      font-weight: 800;
      position: relative;
      top: 85px;
    }
  }

  .document-edit {
    margin-top: 12px;
    display: none;
  }
}
</style>