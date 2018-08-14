<template>
    <div>
        <h1>ADD CARS</h1>
        <form>
           <label>Brand</label> 
           <input v-model="newCar.brand" type="text" placeholder="brand..."><br> 

           <label>Model</label> 
           <input v-model="newCar.model" type="text" placeholder="model..."><br> 

           <label>Year</label> 
           <select v-model="newCar.year">
               <option disabled value="">Please select year</option>
               <option v-for="(year, index) in years" :key="index">{{ year }}</option>
           </select><br>
           

           <label>Max Speed</label> 
           <input v-model="newCar.maxSpeed" type="number" placeholder="max speed..."><br> 

           <label>Number of doors</label> 
           <input v-model="newCar.numberOfDoors" type="number" placeholder="number of doors..."><br>

           <label>Is automatic</label> 
           <input type="checkbox" id="true" value="true" v-model="newCar.isAutomatic">
           <label for="true">Yes</label><br>

           <label>Engine</label> 

           <input type="radio" id="electric" value="Electric" v-model="newCar.engine">
           <label for="electric">Electric</label><br>

           <input type="radio" id="petrol" value="Petrol" v-model="newCar.engine">
           <label for="petrol">Petrol</label><br>

           <input type="radio" id="hybrid" value="Hybrid" v-model="newCar.engine">
           <label for="hybrid">Hybrid</label><br>

           <input type="radio" id="diesel" value="Diesel" v-model="newCar.engine">
           <label for="diesel">Diesel</label><br>

           <button @click="addNewCar()" type="button">Add car</button>

       </form>
    </div>
</template>

<script>
import { cars } from '../services/Cars.js'

export default {
    name: "AddCar",
    data(){
        return {
            years: [],
            newCar: {}
        }
    },
    methods: {
        addNewCar(){
           cars.add(this.newCar)
           .then(response => {this.$router.push('/cars')}) // nakon resolve-a redirektuje na pocetnu '/cars' stranicu
           .catch(err => console.log(err)) // ako catch-uje error onda console.log-ujemo error
        }
    },
    created(){
        for(var i = 1990; i <= 2018; i++){
            this.years.push(i);
        }
    }
    
}
</script>

