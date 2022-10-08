<template>
  <div class="container">
    <h1>Animation</h1>
    <div class="block" :class="{ animateLeft: animateBlockLeft }"></div>
    <button @click="moveLeft">MOVE LEFT</button>

    <br />
    <Transition name="para">
      <p v-if="paraVisibility">Hey this is a paragraph...</p>
    </Transition>
    <button @click="togglePara">Toggle Paragraph</button>

    <br />

    <Transition name="fireball">
      <div class="block" v-if="animateBall"></div>
    </Transition>
    <button @click="toggleFireball">Toggle Fireball</button>

    <br />
    <base-modal :modalVisibility="modalVisibility" @hideModal="hideModal">
      <p>Hey I am a modal</p>
      <button @click="hideModal">Close me</button>
    </base-modal>
    <div>
      <button @click="showModal">Open Modal</button>
    </div>
  </div>
</template>

<script>
import BaseModal from "./components/BaseModal.vue";
export default {
  name: "App",
  components: { BaseModal },
  data() {
    return {
      animateBlockLeft: false,
      paraVisibility: false,
      animateBall: false,
      modalVisibility: false,
    };
  },
  methods: {
    moveLeft() {
      this.animateBlockLeft = !this.animateBlockLeft;
    },
    togglePara() {
      this.paraVisibility = !this.paraVisibility;
    },
    toggleFireball() {
      this.animateBall = !this.animateBall;
    },
    showModal() {
      this.modalVisibility = true;
    },
    hideModal() {
      this.modalVisibility = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  /* margin-top: 60px; */
}

.container {
  margin: 2 rem auto;
  max-width: 40 rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

button {
  background-color: chartreuse;
  padding: 18px;
  color: black;
  border-radius: 10px;
  border: none;
}

button:hover {
  background-color: rgb(52, 216, 52);
  cursor: pointer;
  border: none;
}

/*only keyframes*/

.block {
  height: 200px;
  width: 200px;
  border-radius: 100%;
  background-color: royalblue;
  margin-bottom: 20px;
  /* transition: 0.8s ease-in-out; */
}

.animateLeft {
  /* transform: translateX(-250px); */
  animation: slide-fade 0.8s ease-in-out forwards;
  /* animation-direction: alternate; */
}

@keyframes slide-fade {
  0% {
    transform: translateX(0) scale(1);
  }
  50% {
    transform: translateX(-125px) scale(1.3);
  }
  100% {
    transform: translateX(-250px) scale(1);
  }
}

/* only transition component */

.para-enter-from {
  opacity: 0;
  transform: translateY(-40px);
}

.para-enter-active {
  transition: all 0.5s ease-out;
  /* to use keyframes
  animation: para 0.5s ease-in reverse; */
}

.para-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.para-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.para-leave-active {
  transition: all 0.3s ease-out;
  /* to use keyframes
  animation: para 0.5s ease-in; */
}

.para-leave-to {
  opacity: 0;
  transform: translateY(-40px);
}

@keyframes para {
  0% {
    transform: translateY(0) scale(1);
  }
  50% {
    transform: translateY(-125px) scale(1.3);
  }
  100% {
    transform: translateY(-250px) scale(1);
  }
}

/* transition and keyframes */

.fireball-enter-active {
  animation: fireball 0.8s ease-in-out;
}

.fireball-leave-active {
  animation: fireball 0.5s ease-in reverse;
}

@keyframes fireball {
  0% {
    transform: translateX(0) scale(1);
  }
  50% {
    transform: translateX(-125px) scale(1.3);
  }
  100% {
    transform: translateX(-250px) scale(1);
  }
}
</style>
