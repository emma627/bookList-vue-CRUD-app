<template>
<header>
  <h1>My Book Lists</h1>
  <Button
  :text="showAddBook ? 'Close' : 'Add Book'"
  :color="showAddBook ? 'red' : 'pink'"
  @btn-click="$emit('btn-click')"/>
</header>
</template>

<script>
import Button from './Button'

export default {
name: "Header",
components:{
    Button,
},
props:{
  showAddBook:Boolean
}

}

</script>

<style>
header{
    display:flex;
     align-items: center;
    justify-content: space-between;
}
</style>