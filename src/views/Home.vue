<template>
  <div>
    Burgers
    <Burger v-for="burger in burgers"
            v-bind:burger="burger" 
            v-bind:key="burger.name"/>
  </div>
  <div id="map" v-on:click="addOrder">
    click here
  </div>
</template>

<script>
import Burger from '../components/Burger.vue'
import io from 'socket.io-client'

const socket = io();

function MenuItem(name, lactose, gluten, imgUrl, prop1, prop2, prop3, prop4) {
		this.name = name;
		this.lactose = lactose;
		this.gluten = gluten;
		this.imgUrl = imgUrl;
		this.prop1 = prop1;
		this.prop2 = prop2;
		this.prop3 = prop3;
		this.prop4 = prop4;
		}
		
		const burgerArray = [new MenuItem("The Pixel Burger", true, true, "/img/pixelburger.png", "250x237 pixels", "Contains 100 pixel beef", "Contains pixel", "Optional:"),
		new MenuItem("The Cartoon Burger", true, true, "/img/cartoonburger.webp", "Completely made up", "100% of cartoon beef", "Contains cartoon", "Contains cartoon"),
		new MenuItem("The Alien Burger", false, false, "/img/alienburger.jpg", "An &copy;Aether Burger Inc. Classic!", "Found in the aether", "Ingredients unknown")];
		console.log(burgerArray);

export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: [ {name: "small burger", kCal: 250},
                 {name: "standard burger", kCal: 450},
                 {name: "large burger", kCal: 850}
               ]
    }
  },
  methods: {
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    addOrder: function (event) {
      var offset = {x: event.currentTarget.getBoundingClientRect().left,
                    y: event.currentTarget.getBoundingClientRect().top};
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: event.clientX - 10 - offset.x,
                                           y: event.clientY - 10 - offset.y },
                                orderItems: ["Beans", "Curry"]
                              }
                 );
    }
  }
}
</script>

<style>
  #map {
    width: 300px;
    height: 300px;
    background-color: red;
  }
</style>
