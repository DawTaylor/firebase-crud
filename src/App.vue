<template>
<div id="app">
  <section class="hero">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">
            Simple Firebase CRUD
          </h1>
          <h2 class="subtitle">
            A simple Firebase CRUD using VUE.JS and vanilla JS implementation of Firebase DB
          </h2>
        </div>
      </div>
  </section>
  <div class="container">
    <div class="columns">
      <firebaseForm></firebaseForm>
      <firebaseData></firebaseData>
    </div>
  </div>
</div>
    
</template>

<script>
import FirebaseForm from './FirebaseForm.vue'
import FirebaseData from './FirebaseData.vue'

export default {
  name: 'app',
  components : { FirebaseForm, FirebaseData }
}
</script>

<style>
</style>
