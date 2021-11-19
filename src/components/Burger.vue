<template>
  
   
      <div class="burger">
         <h3>{{ burger.name }}</h3>
         
         
             <img v-bind:src="burger.imgUrl" class="imgBurg">
         
         <ul>
            <li>{{burger.prop1}}</li>
            <li>{{burger.prop2}}</li>
            <li>{{burger.prop3}}</li>
            <li>{{burger.prop4}}</li>
         </ul><br>
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

.burger {
     display: grid;
     grid-gap: 10px;
     grid-template-columns: auto auto auto;
     background: black;
     color: white;
}
 .imgBurg {
     height: 150px;
     width: 200px;
     }

#lactose {
   font-weight: bold;
}
#gluten {
   font-weight: bold;
}


</style>
