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
<div class="orderButtons">
        <button type="submit" v-on:click="addBurger" id="plus">
          +
        </button>
        <h4>{{ amountOrdered }}</h4>
        <button type="submit" v-on:click="removeBurger" id="minus">
          -
        </button>
</div>



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
      if (this.amountOrdered < 0) {
        this.amountOrdered = 0;
      }
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
     margin-left: 5px;
     }

 .orderButtons {
   display: grid;
   grid-gap: 25px;
   grid-template-columns: 20px 20px 20px;
   margin: 0em 2em;
 }

 button {
   width: 40px;
   height: 40px;
 }

 h4 {
   text-align: end;
   margin-left: 15px;
 }


#lactose {
   font-weight: bold;
}
#gluten {
   font-weight: bold;
}


</style>
