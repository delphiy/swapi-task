<template>
  <div class="row">
    <div class="col-12 text-center mt-5 mb-4 text-small">
      <h4>PAGE {{ this.currentPage }}/{{ this.lastPage }}</h4>
      <button class="btn btn-primary-outline mr-2 mt-1">
        <img
          src="@/assets/images/prev-arrow.svg"
          @click="$emit('on-previous-page')"
        />
      </button>
      <button class="btn btn-primary-outline ">
        <img
          src="@/assets/images/next-arrow.svg"
          @click="$emit('on-next-page')"
        />
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      required: true,
    },
    lastPage: {
      required: true,
    },
  },
};
</script>

<style></style>
