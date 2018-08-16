<template>
    <div>
        <h1 v-if="(!this.$route.params.id)">Add car</h1>
        <h1 v-else>Edit car</h1>
        <form @submit.prevent>

            <div class="form-group">
                <label><b>Brand</b></label> 
                <input class="form-control" v-model="newCar.brand" type="text" minlength="2" placeholder="brand..." required>
            </div>
            <div class="form-group">
                <label><b>Model</b></label> 
                <input class="form-control" v-model="newCar.model" type="text" minlength="2" placeholder="model..." required>
            </div>
            <div class="form-group">
                <label><b>Year</b></label><br> 
            <select v-model="newCar.year" required>
                <option disabled value="">Please select year</option>
                <option v-for="(year, index) in years" :key="index">{{ year }}</option>
            </select>
            </div>  
            <div class="form-group">
                <label><b>Max Speed</b></label> 
                <input class="form-control" v-model="newCar.maxSpeed" type="number" placeholder="max speed...">
            </div>
            <div class="form-group">
                <label><b>Number of doors</b></label> 
                <input class="form-control" v-model="newCar.numberOfDoors" type="number" placeholder="number of doors..." required>
            </div>
            <div class="form-group">
                <label><b>Is automatic</b></label><br> 
                <input type="checkbox" id="true" value="true" v-model="newCar.isAutomatic" required>
                <label for="true">Yes</label>
            </div>
                <label><b>Engine</b></label> 
            <div class="form-group">
                <input type="radio" id="electric" value="Electric" v-model="newCar.engine" required>
                <label for="electric">Electric</label>
            </div>
            <div class="form-group">
                <input type="radio" id="petrol" value="Petrol" v-model="newCar.engine" required>
                <label for="petrol">Petrol</label>
            </div>
            <div class="form-group">
                <input type="radio" id="hybrid" value="Hybrid" v-model="newCar.engine" required>
                <label for="hybrid">Hybrid</label>
            </div>
            <div class="form-group">
                <input type="radio" id="diesel" value="Diesel" v-model="newCar.engine" required>
                <label for="diesel">Diesel</label>
            </div>

            <button class="btn-default" style="margin-right: 20px;" v-if="(!this.$route.params.id)" @click="addNewCar()" type="submit">Add car</button>
            <button class="btn-default" style="margin-right: 20px;" v-else @click="edit(newCar)" type="submit">Submit</button>
            <input class="btn-default" style="margin-right: 20px;" type="reset" value="Reset" />
            <!-- elements of type "reset"  are rendered as buttons, 
            with a default click event handler that resets all of the inputs in the form to their initial values. -->
            <button class="btn-default" @click="preview()" type="button">Preview</button>

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
        },
        edit(car) {
            cars.edit(car)
            .then((response) => {
                this.$router.push('/cars')})
            .catch(err => console.log(err))
        },
        preview(){
            alert(`
                brand: ${this.newCar.brand}
                model: ${this.newCar.model}
                year: ${this.newCar.year}
                max speed: ${this.newCar.maxSpeed}
                number of doors: ${this.newCar.numberOfDoors}
                transmition: ${this.newCar.isAutomatic ? "automatic" : "manual"}
                engine: ${this.newCar.engine}`
            )
        }
    },
    created() {
        for (var i = 1990; i <= 2018; i++) {
            this.years.push(i);
        }
        if(this.$route.params.id) {
            cars.getCar(this.$route.params.id)
            .then(response => (this.newCar = response.data));
        }
    }
    
}
</script>

