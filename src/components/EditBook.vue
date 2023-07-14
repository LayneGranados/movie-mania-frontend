<template>
  <div v-if="book" class="edit-book">
    <h4 class="center-align pink-text accent-3">Edit Book</h4>
    <form @submit.prevent="EditBook">
      <div class="field title">
        <label for="title">Title:</label>
        <input type="text" name="title" v-model="book.title" />
      </div>
      <div class="field title">
        <label for="author">Author:</label>
        <input type="text" name="author" v-model="book.author" />
      </div>
      <div class="field title">
        <label for="isbn">Genre:</label>
        <input type="text" name="isbn" v-model="book.genre" />
      </div>
      <div class="field title">
        <label for="language">Language:</label>
        <input type="text" name="language" v-model="book.language" />
      </div>
      <div class="field center-align">
        <button class="btn green">Edit Book</button>
      </div>
    </form>
  </div>
</template>

<script>

</script>

<style>
.edit-book {
  max-width: 700px;
  margin: 0 auto;
}

.edit-book form {
  padding: 30px;
}

.edit-book .btn {
  margin-top: 30px;
}
</style>
