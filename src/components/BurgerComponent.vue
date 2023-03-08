<template>
  <div class="burger-component">
    <transition name="modal"> 
      <div v-if="isOpen">
        <div class="overlay" @click.self="isOpen = false;">
          <div class="modal">
            <h1>Hamburguesa: {{burger.nombre}}</h1>
            <h2>Ingredientes:</h2>
            <h3 v-for="ingrediente in burger.ingredientes" v-bind:key="(ingrediente)">{{ingrediente}}</h3>
            <h2>Calorias: {{burger.calorias}}</h2>
            <button @click="isOpen=false">Salir</button>
          </div>
        </div>
      </div>
    </transition>  
    <button @click="isOpen=!isOpen">{{burger.nombre}}</button>
  </div>

</template>


<script>

export default {
  name: 'BurgerComponent',
  props: ['burger'],
  data() {
    return {
      isOpen: false
    };
  },
}
</script>

<style scoped>
.modal {
  width: 500px;
  margin: 0px auto;
  padding: 20px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px 3px;
  transition: all 0.2s ease-in;
  font-family: Helvetica, Arial, sans-serif;
}
.fadeIn-enter {
  opacity: 0;
}

.fadeIn-leave-active {
  opacity: 0;
  transition: all 0.2s step-end;
}

.fadeIn-enter .modal,
.fadeIn-leave-active.modal {
  transform: scale(1.1);
}

button {
  padding: 7px;
  margin-top: 10px;
  background-color: #256a4b;
  border-radius: 10px;
  box-shadow: 3px 3px 0px 0px #00000033;
  border: none;
  color: white;
  font-size: 1.1rem;
}

button:active{
  background-color: #42b983;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
  background: #00000094;
  z-index: 999;
  transition: opacity 0.2s ease;
}
</style> -->