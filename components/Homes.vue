<template>
  <div>
    <img
      :src="home.images[0]"
      :alt="home.title"
      style="width: 200px; height: 200px;"
    />
    <h2>{{ home.title }}</h2>
  </div>
</template>

<script>
export default {
  props: {
    home: Object
  }
};
</script>
