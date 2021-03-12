<template>
  <div v-for="book in books" :key="book.id" :books="books">
      <Book
      :book="book"
      @toggle-favorite="$emit('toggle-favorite',book.id)"
      @delete-book="$emit('delete-book',book.id)"/>
  </div>
</template>

<script>
import Book from "./Book"
export default {
    name:"Books",
    props:{
        books:Array,
    },
    components:{
        Book,
    }

}
</script>

<style>

</style>