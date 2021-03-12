<template>
  <div class="container">
    <Header @btn-click="btnClick" :showAddBook="showAddBook" />
    <add-book v-if="showAddBook" @add-book="addNewBook" />
    <Books
      @delete-book="deleteBook"
      @toggle-favorite="toggleFavorite"
      :books="books"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import AddBook from "./components/AddBook.vue";
import Books from "./components/Books.vue";
export default {
  name: "App",
  components: {
    Header,
    AddBook,
    Books,
  },
  data() {
    return {
      books: [],
      showAddBook: false,
    };
  },
  methods: {
    btnClick() {
      this.showAddBook = !this.showAddBook;
    },
    async fetchBooks() {
      const res = await fetch("http://localhost:5000/books");
      const data = await res.json();
      return data;
    },
    async fetchBook(id) {
      const res = await fetch(`http://localhost:5000/books/${id}`);
      const data = await res.json();
      return data;
    },
    async addNewBook(newBook) {
      const res = await fetch("http://localhost:5000/books", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(newBook),
      });
      const data = await res.json();
      this.books = [...this.books, data];
    },
    async deleteBook(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`http://localhost:5000/books/${id}`, {
          method: "DELETE",
        });

        res.status === 200
          ? (this.books = this.books.filter((book) => book.id !== id))
          : alert("Error deleting book");
      }
    },
    async toggleFavorite(id) {
      const bookToToggle = await this.fetchBook(id);
      const updateFavorite = {
        ...bookToToggle,
        favorite: !bookToToggle.favorite
      };
      const res = await fetch(`http://localhost:5000/books/${id}`, {
        method: "PUT",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify(updateFavorite),
      });
      const data = await res.json();

      this.books = this.books.map((book) =>
        book.id === id ? { ...book, favorite: data.favorite } : book
      );
    },
  },
  async created() {
    this.books = await this.fetchBooks();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  color: #2c3e50;
  margin-top: 60px;
}
.container {
  max-width: 500px;
  min-height: 300px;
  border: 5px solid steelblue;
  margin: 30px auto;
  padding: 30px;
  border-radius: 1rem;
}
</style>
