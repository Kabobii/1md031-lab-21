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
         <ul>
           <li>{{ amountOrdered }}</li>
         </ul>
        <button type="submit" v-on:click="addBurger" id="plus">
          +
        </button>
        <button type="submit" v-on:click="removeBurger" id="minus">
          -
        </button>
      </div>
  
</template>

<script>
export default {
  name: 'Burger',
  props: {
    burger: Object
  },
  data: function () {
    return {
      amountOrdered: 0,
    }
  },
  methods:  {
    addBurger: function () {
      this.amountOrdered++;
      this.$emit('orderedBurger', { name:   this.burger.name,
            amount: this.amountOrdered
          }
      );
    },
    removeBurger: function () {
      this.amountOrdered--;
      this.$emit('orderedBurger', { name:   this.burger.name,
            amount: this.amountOrdered
          }
      );
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


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
