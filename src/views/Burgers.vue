<template>
  <div class="burgers-viables">
    <ul>
      <li class="burger-links" v-for="burger in burgers" v-bind:key="(burger.id)">
        <BurgerComponent  :burger="burger" />
      </li>
    </ul>
  </div>
</template>

<script>
import BurgerComponent from '@/components/BurgerComponent.vue'

export default {
  name: 'Burgers',
  data() {
    return {
      burgers: 'No hay hamburguesas disponibles',
    };
  },
  components: {
    BurgerComponent
  },
  methods: {
    getBurgers() {
      this.$http.get('https://hamburguesas-back.elevadev.cl/burger/')
        .then((response) => { this.burgers = response.data; },
        err => console.log(err));
    },
  },
  created() {
    console.log('Api rest used');
    this.getBurgers();
  },
}
</script>

<style>
</style>
