<template>
  <div class="dialog-window">
    <div id="prompt-form">
      <div class="message">Подтвердите изменение</div>
      <button class="submit" @click="$emit('confirmChange', index)">Подтвердить</button>
      <button class="cancel" @click="$emit('cancelChange')">Отмена</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DialogWindow',
  
  props: {
    index: Number,
  }
}
</script>