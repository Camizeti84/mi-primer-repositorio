
<script setup>
import {ref,computed} from 'vue';


 const name="pequenajo canijoo";
 const styleColor="color:blue";
 const arrayColores=["blue","red","peru","teamo"];
 const activo=null;
 const count= ref(0);
 const arrayNumber=ref([]);
 const arrayFrutas=[
  {name:'platano',
   price:10,
   description:'un platano'
  },
  {name:'manzana',
   price:5,
   description:'una manzana'
  },
  {name:'limon',
   price:6,
   description:'un limon'
  }
];
const objetoFruta={ name:'platano',
                    price:10,
                    description:'un platano'
                    }
 
 const handleClick=(message)=>{
  console.log(message);
 }
 const increment=()=>{
  console.log('muy bien increment');
  count.value++;
 }
 const decrement=()=>{count.value--}

 const classcomputed=computed(()=>{
    if (count.value == 0) {return 'zero'} 
    if (count.value > 0) {return 'positivo'} 
    if (count.value < 0) {return 'negativo'} 
 });
 const add=()=>{arrayNumber.value.push(count.value);};//ingresa el num count al array
 const statebtn=computed(()=>{
    const numsearch= arrayNumber.value.find((num)=> num ===count.value);
    if(numsearch===0) return true;
    return numsearch ? true : false
 });



</script>

<template>
  <h1 :class="classcomputed">hola {{ name.toUpperCase()}}</h1>
  <h2>{{arrayColores}} </h2>
  <h2 :style="'color: ${arrayColores[2]}'">soy peruano</h2>
  <h2>{{ activo ? "estoy activo" : "estoy inactivo" }}</h2>
  <h2 v-if="activo">estoy activo</h2>
  <h2 v-else-if="activo===false">estoy inactivo</h2>
  <h2 v-else>estoy indesiso</h2>
  <ul class="list-group">
    <li class="list-group-item" v-for="(fruta,index) in arrayColores" :key="index">
   {{ index }} - {{ fruta }}
    </li>
  </ul>
  <ul class="list-group">
    <li class="list-group-item" v-for="fruta in arrayFrutas" :key="fruta.name">
      <span v-if="fruta.price > 5">
        {{ fruta.name }} - {{ fruta.price }}- {{ fruta.description }}  
      </span>
     
    </li>
  </ul>
  <ul class="list-group mt-4">
    <li class="list-group-item" v-for="(value,propiedad,index) in objetoFruta" :key="index">
      {{ index }} : {{ propiedad }} : {{ value }} 
    </li>
  </ul>
  <div class="container">
      <button v-on:click.right="handleClick('pepe')" class="btn btn-success">Activame</button>
      <button @click="handleClick('pepepepep')"  class="btn btn-info">Activame</button>   
      <button @click="increment()"  class="btn btn-danger">incrementar</button>
      <button @click="decrement()"  class="btn btn-secondary">disminuir</button>
  </div>    
  <h2>{{ count }}</h2>

  <button @click="add" :disabled="statebtn">Agregar</button>
  <br>
  <h2>{{ arrayNumber }}</h2>


</template>


<style>
  h1{
    color: blue;
  }
  .zero{color: rgb(0, 255, 4);}
  .positivo{color: blue;}
  .negativo{color:peru;}
  
</style>
