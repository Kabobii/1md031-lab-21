<template>
  <div>
  <div class="burger">
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

.burger {
    
    padding: 15px;
    background-color: black;
    color: white;
    border-radius: 5px;
    font-size: 150%;
}

#lactose {
   font-weight: bold;
}
#gluten {
   font-weight: bold;
}


</style>
