<template>
  <div class="card">
      <div class="card-header">
          <h5 class="card-title">{{titulo}}</h5>
      </div>
      <div class="card-body">
          <slot> </slot>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Painel',
  props: {
    titulo: String
  }
}
</script>