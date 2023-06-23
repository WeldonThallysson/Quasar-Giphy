<template>
  <q-page>
    <headerSearch />
  </q-page>
</template>

<script>
import { defineComponent } from "vue";
import headerSearch from "../components/headerSearch/index.vue";

export default defineComponent({
  name: "IndexPage",
  components: {
    headerSearch,
  },
});
</script>
