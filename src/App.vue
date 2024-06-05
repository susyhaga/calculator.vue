<script setup>
  import{reactive} from 'vue';

  const estado = reactive({
    filter:'',
    num1:'',
    num2:'',
  })

  const sub =({num1,num2})=>{
    return num1-num2
  };
  const add=({num1,num2})=>{
    return num1+num2
  };
  const mult=({num1,num2})=>{
    return num1*num2
  };
  const div=({num1,num2})=>{
    return num1/num2
  };

  function capturaValor1(evento){
    estado.num1 = evento.target.value
  }
  function capturaValor2(evento){
    estado.num2 = evento.target.value
  }

  const result =() => {
    const{num1, num2, filter} = estado
    if (num1 !== '' && num2 !== '') {
    switch (filter) {
      case '+':
        return add({ num1: parseFloat(num1), num2: parseFloat(num2) });
      case '-':
        return sub({ num1: parseFloat(num1), num2: parseFloat(num2) });
      case 'x':
        return mult({ num1: parseFloat(num1), num2: parseFloat(num2) });
      case '÷':
        return div({ num1: parseFloat(num1), num2: parseFloat(num2) });
    }
  }
  return '';
  };

  function filterChange(evento){
    estado.filter = evento.target.value
  }
</script>

<template>
  <div class="container">
    <header>
      <h1 class="p-5 mb-4 mt-4 bg-dark text-white text-center rounded-4">Calculator</h1>
    </header>
</div>

  <form>
  <div class="container"> 
    <div class="row">
      <div class="col-3 ms-4">
        <p>Choose an operation</p>
      </div>
      <div class="col-8">
        <select v-model="estado.filter" @change="filterChange" name="filter" id="filtro">
          <option value="+">+</option>
          <option value="-">-</option>
          <option value="x">x</option>
          <option value="÷">÷</option>
        </select>
      </div>
    </div>
    <div class="row">
      <div class="col-3 m-3">
        <input @keyup="capturaValor1" type="number" class="form-control" placeholder=" type a number">
      </div>
      <div class="col-1 mt-3">
        <h2 class="text-center">{{estado.filter}}</h2>
      </div>
      <div class="col-3 mt-3 gap-2">
        <input @keyup="capturaValor2" type="number" class="form-control" placeholder=" type a number">
      </div>
      <div class="col-1 mt-3">
        <h2 class="text-center">=</h2>
      </div>
        <div class="col-3 m-3 " id="borda">
          <span class="mt-3">{{result()}}</span>
        </div>
      </div>
    </div>
  </form>
</template>

<style scoped>
#borda{
  border: 3px solid #000;
  border-radius: 10px;
}
</style>
