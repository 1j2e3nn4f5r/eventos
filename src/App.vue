<template>
  <div id="app">
    <div class="container">
      <div class="row mt-5 justify-content-center">
        <div class="col-md-10">
          <div class="card border border-dark">
          <div class="card-body">
            <router-view />
          </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
