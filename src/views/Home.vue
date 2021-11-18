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
  
     <header class="headliner">
         <img src="/img/topimage.jpg" id="headimg">
         <h1 id="headline">Welcome to Digital Burger's</h1>
		
   </header>
   <main>
      <section class="ingredients" id="burgers">
      <div class="wrapper">
      <div class="burger head">
         <h2>Select Burger</h2>
         <span>This is where you execute burger</span><br>
         </div>
         <div class="burger pixel">
         <!-- Första burgarn -->
         <h3>The Pixel Burger</h3><img src="/img/pixelburger.png"
         alt="A pixel burger" title="A pixel burger" style="width: 200px;height: 150px;">
         
         <ul>
            <li>250x237 pixels</li>
            <li>Contains 100 pixel beef</li>
            <li>Contains pixel <span id="lactose">lactose</span></li>
            <li>Optional: <span id="gluten">Gluten free</span></li>
		</ul><br>
		</div>
		<div class="burger cartoon">
		<!-- Andra burgarn -->
         <h3>The Cartoon Burger</h3><img src="/img/cartoonburger.webp"
         alt="A cartoon burger" title="A cartoon burger" style="width: 200px;height: 150px;">
         <ul>
            <li>Completely made up</li>
            <li>100% of cartoon beef</li>
            <li>Contains cartoon <span id="lactose">lactose</span></li>
            <li>Contains cartoon <span id="gluten">gluten</span></li>
		</ul><br>
		</div>
		<div class="burger alien">
		<!-- Tredje burgarn -->
		<h3>The Alien Burger</h3><img src="/img/alienburger.jpg"
         alt="An alien burger" title="An alien burger" style="width: 200px;">
         
         <ul>
            <li>An &copy;Aether Burger Inc. Classic!</li>
            <li>Found in the aether</li>
            <li>Ingredients <span id="unknown">unknown</span></li>
		</ul><br>
		</div>
		</div>
      </section>
      <section id="contact">
         <h2>Customer Information</h2><span>This is where you provide some info about yourself</span><br>
         <form>
         <p>
            <label for="fullname">First</label><br>
            <input type="text" id="fullname" name="fn" required="required" placeholder="First- and Last name">
		</p>
		<p>
			<label for="E-mail">E-mail</label><br>
            <input type="email" id="email" name="em" required="required" placeholder="E-mail address">
		</p>
		<p>
            <label for="Street">Street</label><br>
            <input type="text" id="streetname" name="sn" placeholder="Street name">
		</p>
		<p>
            <label for="House">House</label><br>
            <input type="number" id="housenumber" name="hn" placeholder="House number">
		</p>
		<p>
            <label for="payment">Payment options</label><br>
            <select id="payment" name="pym">
                <option>Swish</option>
                <option>Credit card</option>
                <option>Invoice</option>
                <option>Exchange trade</option>
            </select>
		</p>
		<p>
            <label for="Gender">Gender</label><br>
            <input type="radio" id="gender" name="ge" value="Alien">
            <label for="Gender">Alien</label><br>
            <input type="radio" id="gender" name="ge" value="Female">
            <label for="Gender">Female</label><br>
            <input type="radio" id="gender" name="ge" value="Male">
            <label for="Gender">Male</label><br>
            <input type="radio" id="gender" name="ge" value="Non-binary">
            <label for="Gender">Non-binary</label><br>
            <input type="radio" id="gender" name="ge" value="Undefined">
            <label for="Gender">Undefined</label><br>
		</p>
		</form>
      </section>
      <button type="submit">
        <img src="/img/subburger.jpg"
        alt="Sub burger" title="Sub burger" style="width: 20px;height:20px;">
        Submit order
      </button>
   </main>
   <hr>
   <footer>
      <p>&copy; Aether Burger Inc.</p>
      </footer>
  
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
      burgers: burgerArray
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
