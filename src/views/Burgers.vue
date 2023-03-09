<template>
  <div class="burgers-viables">
    <div  class="burger-links">
      <h1>The burgers avaible!</h1>
      <ul class="burger-list">
        <li v-for="burger in burgers" v-bind:key="(burger.id)">
          <BurgerComponent  :burger="burger" />
        </li>
      </ul>
    </div>
    <CreateBurgerComponent/>
  </div>
</template>

<script>
import BurgerComponent from '@/components/BurgerComponent.vue'
import CreateBurgerComponent from '../components/CreateBurgerComponent.vue';

export default {
  name: 'Burgers',
  data() {
    return {
      burgers: 'No hay hamburguesas disponibles',
    };
  },
  components: {
    BurgerComponent,
    CreateBurgerComponent,
  },
  methods: {
    getBurgers() {
   
    this.$http.get('https://hamburguesas-back.elevadev.cl/burger/')
        .then((response) => { this.burgers = response.data; },
        err => console.log(err));
    },
  },
  created() {
    this.getBurgers();
    console.log('Api rest used');
  },
}
</script>

<style scoped>
li{
  list-style: none;
}

.burgers-viables{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.burger-links{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background-color: aquamarine;
  border-radius: 10px;
  box-shadow: 5px 5px 10px 0px #00000033;
  width: 40vw;
}

.burger-list{
  display: flex;
  flex-direction: column;
  align-items: center;
  align-content: center;
  justify-content: center;
  margin: 0;
  padding: 10px;
  width: 40vw;
  
}

</style>
