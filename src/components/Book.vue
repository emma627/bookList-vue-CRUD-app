<template>
  <div @dblclick="$emit('toggle-favorite',book.id)"
  :class="[book.favorite ? 'favorite' : '', 'book']">
    <h3>
      {{ book.name }}
      <i @click="deleteBook(book.id)" class="fas fa-times"></i>
    </h3>
    <p>Author:{{ book.author }}</p>
  </div>
</template>

<script>
export default {
  name: "Book",
  emits:["delete-book"],
  props: {
    book: Object,
  },
  methods:{
    deleteBook(id){
      this.$emit("deleteBook",id)
    }
  }
};
</script>

<style>
.fas {
  color: red;
}

.book {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.book.favorite {
  background: pink;
}

.book h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>
