<template>
  
      <div class="wrapper">
      <div class="burger pixel cartoon alien">
         <h3>{{ burger.name }}</h3>
         
         
             <img v-bind:src="burger.imgUrl">
         
         <ul>
            <li>{{burger.prop1}}</li>
            <li>{{burger.prop2}}</li>
            <li>{{burger.prop3}}</li>
            <li>{{burger.prop4}}</li>
         </ul><br>
     </div>
  </div>
</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.wrapper {
     display: grid;
     grid-gap: 10px;
     grid-template-rows: 30% 60%;
     grid-template-columns: 33% 33% 33%;
     background: black;
     color: white;
}


.burger {
    padding: 15px;
    background: red;
    color: white;
    border-radius: 5px;
    font-size: 150%;
}

 .pixel {
    grid-column: 1;
    grid-row: 2 ;
 }
 .cartoon {
    grid-column: 2;
    grid-row: 2 ;
 }
 .alien {
    grid-column: 3;
    grid-row: 2 ;
 }
 


#lactose {
   font-weight: bold;
}
#gluten {
   font-weight: bold;
}


</style>
