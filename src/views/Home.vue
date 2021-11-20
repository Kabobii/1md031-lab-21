<template>
  

  
     <header class="headliner">
         <img src="/img/topimage.jpg" id="headimg">
         <h1 id="headline">Welcome to Digital Burger's</h1>
		
     </header>
   
   <main>
   
      <section class="burgers">
         <h2>Select Burger</h2>
         
     <div class="burgermenu">
       
       <Burger v-for="burger in burgers"
            v-bind:burger="burger" 
            v-bind:key="burger.name"
               v-on:orderedBurger="addToOrder($event)"/>
     </div>

      </section>
      
      <section id="contact">
         <h2>Customer Information</h2><span>This is where you provide some info about yourself</span><br>
         <form>
         <p>
            <label for="fullname">First</label><br>
            <input type="text" id="fullname" v-model="fulln" required="required" placeholder="First- and Last name">
		</p>
		<p>
			<label for="E-mail">E-mail</label><br>
            <input type="email" id="email" v-model="mail" required="required" placeholder="E-mail address">
		</p>
           <div id="mapWrapper">
           <div id="map" v-on:click="setLocation">
             <div v-bind:style="{ left: location.x + 'px',
                                   top: location.y + 'px' }">
             T
             </div>
           </div>
           </div>

		<p>
            <label for="payment">Payment options</label><br>
            <select id="payment" v-model="payme">
                <option>Swish</option>
                <option>Credit card</option>
                <option>Invoice</option>
                <option>Exchange trade</option>
            </select>
		</p>
		<p>
            <label for="Gender">Gender</label><br>
            <input type="radio" id="gender" v-model="genders" value="Alien">
            <label for="Gender">Alien</label><br>
            <input type="radio" id="gender" v-model="genders" value="Female">
            <label for="Gender">Female</label><br>
            <input type="radio" id="gender" v-model="genders" value="Male">
            <label for="Gender">Male</label><br>
            <input type="radio" id="gender" v-model="genders" value="Non-binary">
            <label for="Gender">Non-binary</label><br>
            <input type="radio" id="gender" v-model="genders" value="Undefined">
            <label for="Gender">Undefined</label><br>
		</p>
		</form>
      </section>
      <button v-on:click="subbutton" type="submit">
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
import menu from '../assets/menu.json'


const socket = io();

/*function MenuItem(name, lactose, gluten, imgUrl, prop1, prop2, prop3, prop4) {
		this.name = name;
		this.lactose = lactose;
		this.gluten = gluten;
		this.imgUrl = imgUrl;
		this.prop1 = prop1;
		this.prop2 = prop2;
		this.prop3 = prop3;
		this.prop4 = prop4;
		}
		
		const burgerArray = [new MenuItem("The Pixel Burger", true, true, "/img/pixelburger.png", "250x237 pixels", "89% of pixel beef", "Contains pixel lactose", "Optional: gluten free"),
		new MenuItem("The Cartoon Burger", true, true, "/img/cartoonburger.webp", "Completely made up", "100% of cartoon beef", "Contains cartoon lactose", "Contains cartoon gluten"),
		new MenuItem("The Alien Burger", false, false, "/img/alienburger.jpg", "An &copy;Aether Burger Inc. Classic!", "Found in the aether", "Ingredients unknown")];
		console.log();*/

export default {
  name: 'Home',
  components: {
    Burger
  },
  data: function () {
    return {
      burgers: menu,
      orderedBurgers: {},
      location: { x:0,
                  y:0
      },
      fulln: "",
      mail: "",
      payme: "",
      genders: ""
    }
  },
  methods: {
    addToOrder: function (event) {
      this.orderedBurgers[event.name] = event.amount;
      console.log(this.orderedBurgers)
    },
    getOrderNumber: function () {
      return Math.floor(Math.random()*100000);
    },
    setLocation: function (event) {
      const setPos = event.target.getBoundingClientRect();
      this.location.x = event.clientX-setPos.left-10;
      this.location.y = event.clientY-setPos.top-10;
    },
    subbutton: function() {
      console.log(this.$data);
      socket.emit("addOrder", { orderId: this.getOrderNumber(),
                                details: { x: this.location.x,
                                           y: this.location.y },
                             orderItems: ["Beans", "Curry"]
          }
      );
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
      /*var setPos = event.target.getBoundingClientRect();
      this.location.x = event.clientX-setPos.left-10;
      this.location.y = event.clientY-setPos.top-10;
      socket.emit("addOrder", { details: { x: this.location.x,
                                           y: this.location.y}
         }
      )*/
    },

  }
}
</script>

<style>
  #map {
    width: 1920px;
    height: 1078px;
    background: url("/img/polacks.jpg");
    position: relative;
  }
  #map div {
    position: absolute;
  }
  
  #mapWrapper {
    width: 90vw;
    height: 40vw;
    left: 3%;
    overflow: scroll;
  }


body {
   font-family: courier new;
}

.headliner {
    padding: 5px 8px;
}

#headline {
    position: absolute;
    margin: 10px 100px;
    margin-top: -350px;
    font-weight: bold;
    font-size: 5em;
    text-align: center;
}

header {
    overflow: hidden;
}

#headimg {
    width: 100%;
    height: 350px;
    opacity: 50%;
        /*margin-top: -100%;*/
}


.burgers {
    background: black;
    border: 2px dashed yellow;
    padding: 5px 10px;
    margin: 5px 5px;
    color: white;
}

.burgermenu {
    display:grid;
    grid-gap: 10px;
    grid-template-columns: auto auto auto;
    }


#contact {
    border: 2px dashed black;
    padding: 5px 10px;
    margin: 5px 5px;
}

button {
    margin: 10px 0px;
}
button:hover {
   background: cornflowerblue;
   cursor: alias;
}
  
</style>
