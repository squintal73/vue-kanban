<template>
  <div class="tile" :class="{checked: todoW.checked}">
    <div class="tile-icon">
      <i class="icon" :class="todoW.checked ? 'icon-check' : 'icon-time'"></i>
    </div>
    <div class="tile-content">
      <p class="tile-subtitle">{{ todoW.description }}</p>
    </div>
    <div class="tile-action">
      <button @click="$emit('toggle', todoW)" class="btn btn-link">
        <span v-if="todoW.checked">Desmarcar</span>
        <span v-else>Concluído</span>
      </button>
      <button @click="$emit('remove', todoW)" class="btn btn-link">
        <span class="text-error">Remover</span>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todoW: { type: Object, required: true }
  }
};
</script>

<style scoped>
.checked {
  text-decoration: line-through;
  color: lightgray;
}
</style>

