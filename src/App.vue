<template>
  <div id="app">
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'app',
  components: {
    Calculator
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2e3a41;
  margin-top: 60px;
}

.calc {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2e3a41;
  width: 50%;
  height: 28rem;
  margin: auto;
  background-color: #2e3a41;
  box-shadow: 4px 4px 5px rgb(229, 229, 229);
  border-radius: 10px !important;
}

.screen {
  text-align: right;
  color: #2e3a41;
  width: 90%;
  height: 7rem;
  margin: auto auto;
  background-color: #80ac83;
  border-radius: 10px !important;
  font-size: 2.5rem;
}

.btn-shrt{
  width: 30%;
  margin: 0.25rem;
  height: 30%;
  background-color: #d15f41;
  border: none;
  box-shadow: 2px 2px 2px gray;
  font-weight: 900;
  font-size: 1.15rem;
}

.btn:disabled,
.btn:focus,
.btn:active,
.btn:hover {
  outline: none !important;
  box-shadow: none;
  background-color: #8c2420;
  opacity: 1 !important;
}

@media (max-width: 768px) {
  .calc {
    width: 75%;
    height: 28rem;
  }
}

@media (max-width: 360px) {

.screen {
  width: 100%;
  font-size: 2rem;
}

  .btn-shrt{
    width: 27%;
    font-size: 1rem;
  }
}

@media (max-width: 324px) {
  #app {
    display: none;
  }

}
</style>
