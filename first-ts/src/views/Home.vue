<template>
  <div class="home">
    <hello></hello>
  </div>
</template>

<script lang="ts">
import Hello from "@/components/Hello.vue";
import { Component, Vue } from "vue-property-decorator";

@Component({
  components: {
    Hello
  }
})
export default class Home extends Vue {}
</script>
