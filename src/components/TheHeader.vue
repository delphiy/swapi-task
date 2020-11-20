<template>
  <div class="row">
    <div class="col-12 text-center">
      <img
        alt="Vue logo"
        src="@/assets/images/star-wars-logo.png"
        class="text-center"
      />
      <h4 v-if="this.selectedLength == 0">SELECT 3 CHARACTERS!</h4>
      <h4 v-else>YOU HAVE SELECTED {{ selectedNames }}</h4>
      <button
        class="btn-success mr-2 pl-3 pr-3 mt-1"
        @click="$emit('on-download')"
        v-if="this.selectedLength"
      >
        DOWNLOAD
      </button>
      <button
        class="btn-danger pl-3 pr-3"
        @click="$emit('on-reset')"
        v-if="this.selectedLength"
      >
        RESET
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    selectedLength: {
      required: true,
    },
    selectedNames: {
      required: true,
    },
  },

  // computed: {
  //   selectedNames() {
  //     var authors = ["some author", "another author", "last author"];
  //     var authorString = authors
  //       .map(function(author) {
  //         return author.name;
  //       })
  //       .join(",");
  //     return authorString;
  //   },
  // },
};
</script>

<style></style>
