<template>
  <form @submit.prevent="onSubmit" class="add-form">
    <div class="form-control">
      <label>BOOK</label>
      <input type="text" v-model="book" name="author" placeholder="Add Book" />
    </div>
    <div class="form-control">
      <label>Author</label>
      <input
        type="text"
        v-model="author"
        name="author"
        placeholder="Author"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set To Favorite</label>
      <input type="checkbox" v-model="favorite" name="favorite" />
    </div>

    <input type="submit" value="Save Book" class="btn btn-block" 
    />
  </form>
</template>

<script>
export default {
name: "AddBook",
emits:["add-book"],
data(){
  return{
    book:"",
    author:"",
    favorite:false,
  }
},
  methods:{
    onSubmit(){
      const newBook = {
        name:this.book,
        author:this.author,
        favarite:this.favarite
      }
      this.$emit("add-book",newBook)

      this.book="",
      this.author="",
      this.favorite=false
    }

  }
}

</script>

<style>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>