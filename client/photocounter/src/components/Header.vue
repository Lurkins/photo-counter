<template>
  <div class="container">
      <div class="row">
          <div class="col-12">
              <div class="w-100 vh-25 text-center">
                <h1 class="my-3">{{heading}}</h1>
              </div>
          </div>
      </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Header extends Vue {
  @Prop() private heading!: string;

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
