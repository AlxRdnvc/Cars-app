<template>
    <div>
        <h1>CARS</h1>
        <table class="table">
            <thead>
                <tr>
                    <th>brand</th>
                    <th>model</th> 
                    <th>year</th>
                    <th>max speed</th>
                    <th>transmission</th> 
                    <th>engine</th>
                    <th>number of doors</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(car, index) in cars" :key="index">
                    <td>{{ car.brand }}</td>
                    <td>{{ car.model }}</td> 
                    <td>{{ car.year }}</td>
                    <td>{{ car.maxSpeed }}</td>
                    <td>{{ car.isAutomatis ? "Automatic" : "Manual" }}</td> 
                    <td>{{ car.engine }}</td>
                    <td>{{ car.numberOfDoors }}</td>
                    <router-link :to="{ name: 'edit-car', params: { id: car.id } }" class="btn btn-default">
                        <button type="button" class="btn btn-default">Edit</button>
                    </router-link>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

import { cars } from '../services/Cars.js'

export default {
  data() {
    return {
      cars: []
    }
  },
  beforeRouteEnter (to, from, next) {
    cars.getAll()
      .then((response) => {
          next((vm) => {
            vm.cars = response.data
          })
    })
  }
}
</script>