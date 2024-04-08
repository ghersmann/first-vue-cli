<template>
  <tr class="table-item__table-row">
    <td>{{ title }}</td>
    <td>{{ isbn }}</td>
    <td>
      <slot
        name="actionCol"
        :title="title"
        :isbn="isbn"
        :isBookmarked="isBookmarked"
      />
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    title: String,
    isbn: String,
    isBookmarked: Boolean,
  },
  computed: {
    bookMarkedBtnText() {
      return this.isBookmarked ? "Remove Bookmark" : "Add Bookmark";
    },
  },
  methods: {
    handleBookMarkButtonClick() {
      this.$emit("bookmark-clicked", this.isbn);
    },
  },
};
</script>

<style scoped>
.table-item__table td {
  padding: 12px 15px;
}
</style>
