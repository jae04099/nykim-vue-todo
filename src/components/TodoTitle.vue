<template>
  <div class="title">
    <p class="title__message">{{ message }}</p>
    <p class="title__task">You've got</p>
    <span class="title__task-total">{{ taskTotal }}</span> tasks today.
  </div>
</template>
<script>
export default {
  data() {
    return {
      message: "hello Lena!",
      taskTotal: 4,
    };
  },
};
</script>