<template>
  <div>
    <div v-for="home in homes" :key="home.objectID">
      <NuxtLink :to="`home/${home.objectID}`">
        <Homes :home="home" />
      </NuxtLink>
    </div>
  </div>
</template>

<script>
import homes from "~/data/homes";
import Homes from "~/components/Homes.vue";

export default {
  head() {
    return {
      title: "Rent Home",
      meta: [
        {
          name: "description",
          content: "rent, home, good",
          hid: "uniq"
        }
      ]
    };
  },
  data() {
    return {
      homes: homes
    };
  },
  components: {
    Homes
  }
};
</script>
