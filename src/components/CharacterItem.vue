<template>
  <div
    class="col-6 col-sm-6 col-md-4 mb-3 mt-3 cursor-pointer"
    @click="selectCharacter"
  >
    <div
      class="d-md-flex align-items-center ml-3"
      :class="[character.isSelected ? 'bg-primary' : 'bg-white']"
    >
      <div class="border-right p-1">
        <img
          alt="Vue logo"
          src="@/assets/images/profile-placeholder.jpg"
          class="text-center"
          width="100%"
        />
      </div>
      <div class="ml-3 d-block text-center">
        <span class="text-dark">{{ character.name }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    character: {
      required: true,
    },
  },
  methods: {
    selectCharacter() {
      this.$emit("on-select-character", this.character);
    },
  },
};
</script>

<style></style>
