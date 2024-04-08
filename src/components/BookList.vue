<template>
  <section class="table-item">
    <h2 class="table-item__hl">All Books</h2>
    <table class="table-item__table">
      <thead>
        <tr>
          <th class="table-item__table-head-name">Name</th>
          <th class="table-item__table-head--isbn">ISBN</th>
          <th class="th.table-item__table-head--actions">Action</th>
        </tr>
      </thead>
      <tbody>
        <BookListRow
          v-for="book in books"
          :key="book.isbn"
          :title="book.title"
          :isbn="book.isbn"
          :isBookmarked="book?.isBookmarked"
          @bookmark-clicked="handleBookmarkClick"
          class="table-item__table-row"
        >
          <template #actionCol="slotProps">
            <BaseButton
              variant="secondary"
              @btn-clicked="handleBookmarkClick(slotProps.isbn)"
            >
              <svg
                v-if="!slotProps?.isBookmarked"
                style="width: 0.8rem; line-height: 1"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M10 18a8 8 0 100-16 8 8 0 000 16zm1-11a1 1 0 10-2 0v2H7a1 1 0 100 2h2v2a1 1 0 102 0v-2h2a1 1 0 100-2h-2V7z"
                  clip-rule="evenodd"
                />
              </svg>
              <svg
                v-else
                xmlns="http://www.w3.org/2000/svg"
                style="width: 0.8rem; line-height: 1"
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z"
                  clip-rule="evenodd"
                />
              </svg>
              {{ bookMarkedBtnText(slotProps?.isBookmarked) }}
            </BaseButton>
          </template>
        </BookListRow>
      </tbody>
    </table>
  </section>
</template>

<script>
import BookListRow from "@/components/BookListRow.vue";
import BaseButton from "@/components/BaseButton.vue";

export default {
  props: ["books"],
  components: {
    BaseButton,
    BookListRow,
  },
  methods: {
    bookMarkedBtnText(isBookmarked) {
      return isBookmarked ? "Remove Bookmark" : "Add Bookmark";
    },
    handleBookmarkClick(isbn) {
      const currentBookIndex = this.books.findIndex(
        (book) => book.isbn === isbn
      );
      const currentBook = this.books[currentBookIndex];
      currentBook.isBookmarked = !currentBook.isBookmarked ? true : false;
    },
  },
};
</script>

<style scoped>
.table-item__table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 0.9em;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
  width: 100%;
}

.table-item__table-head-name {
  width: 65%;
}

.table-item__table-head-isbn {
  width: 20%;
}

.table-item__table-head-actions {
  width: 15%;
}

.table-item__table-row button {
  opacity: 0.8;
  padding: 5px;
  transition: opacity 500ms;
  cursor: pointer;
  border-radius: 5px;
}

.table-item__table-row:hover button {
  opacity: 1;
}

.table-item__table thead tr {
  background-color: var(--primary);
  color: #ffffff;
  text-align: left;
}

.table-item__table th {
  padding: 12px 15px;
}

.table-item__table tbody tr {
  border-bottom: 1px solid #dddddd;
}

.table-item__table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}

.table-item__table tbody tr:last-of-type {
  border-bottom: 2px solid var(--primary);
}

.table-item__table tbody tr.active-row {
  font-weight: bold;
  color: var(--primary);
}

.table-item__hl {
  margin-top: 1rem;
  padding-bottom: 0.4rem;
  border-bottom: 2px solid var(--primary-dark);
}
</style>
