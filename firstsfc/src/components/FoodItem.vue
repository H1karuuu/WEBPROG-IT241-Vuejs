<template>
    <div class="Apple">
        <h2>{{ name }}</h2>
        <p>{{ message }}</p>
    </div>
</template>

<script>
export default {
    data() {
        return {
            name: 'Apple',
            message: 'I love Apples'
        }
    }
};
</script>

<style>
  .santol {
    border: dashed black 1px;
    display: inline-block;
    margin: 10px;
    padding: 10px;
    background-color: #b40303;
  }

</style>     