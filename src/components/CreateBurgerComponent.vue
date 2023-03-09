<template>
  <div>
    <div class="button-create">
      <transition name="modal"> 
        <div v-if="isOpenModal">
        <div class="overlay" @click.self="isOpenModal = false;">
          <div class="modal">
          <form @submit="setBurger" v-if="isSent">
            <label for="">Nombre de la hamburguesa: </label>
            <input type="text" v-model="burger.name" required>
            <br/>
            <label for="">Primer ingrediente: </label>
            <input type="text" v-model="burger.ingredients[0]" required>
            <br/>
            <label for="">Segundo ingrediente: </label>
            <input type="text" v-model="burger.ingredients[1]">
            <br/>
            <label for="">Tercer ingrediente: </label>
            <input type="text" v-model="burger.ingredients[2]">
            <br/>
            <label for="">Cuarto ingrediente: </label>
            <input type="text" v-model="burger.ingredients[3]">
            <br/>
            <label for="">Calorias: </label>
            <input type="number" v-model="burger.calories" required>
            <br/>
            <input class="button" type="submit" value="Enviar">
            <button @click="isOpenModal=false">Cancelar</button>
          </form>
          <div class="burgerSent" v-if="!isSent">
            <h1>Se envio la hamburguesa correctamente</h1>
            <button @click="isOpenModal=false">Salir</button>
          </div>
          </div>
        </div>
        </div>
      </transition>
      <button @click="reset()">Create a new burger!</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      isOpenModal: false,
      isSent: false,
      burger: {
        name: '',
        ingredients: [],
        calories: null,
      }
    };
  },
  methods: {
    reset(){
      this.isOpenModal = !this.isOpenModal
      this.isSent = !this.isSent
      this.burger.name = ''
      this.burger.ingredients = []
      this.burger.calories = null
    },
    setBurger(e){
      e.preventDefault();
      console.log(this.burger)
      this.burger.ingredients.filter(a => a!=='');

      const formData = new FormData()
      formData.append('nombre',this.burger.name)
      formData.append('ingredientes',this.burger.ingredients)
      formData.append('calorias',this.burger.calories)
      
      this.sentBurgers(formData)
      console.log(this.burger)

      this.reset()
    },
    sentBurgers(formData) {
   
    fetch('https://hamburguesas-back.elevadev.cl/burger/',{
      method: 'POST',
      body: formData
    }).then((res) => res.json())
      .then((res) => console.log(res))
   },
  }
}
</script>
<style>
button,.button {
  padding: 7px;
  margin: 10px;
  background-color: #256a4b;
  border-radius: 10px;
  box-shadow: 3px 3px 3px 0px #00000033;
  border: none;
  color: white;
  font-size: 1.1rem;
}

button:active{
  background-color: #42b983;
}

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
</style>