<template>
  <div class="hello container px-4 mx-auto">
    <h1>{{ msg }}</h1>
    <div class="border border-black-600">
    <p class="text-blue-700 text-left">Choose a car:</p>
    <select class="form-select mt-1 w-full" name="cars" id="cars">
      <option value="lamborghini">Lamborghini</option>
      <option value="ferrari">Ferrari</option>
      <option value="mercedes">Mercedes</option>
      <option value="Porsche">Porsche</option>
    </select>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
