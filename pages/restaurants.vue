<template>
  <main class="container restaurant">
    <div class="restaurantheading">
      <h1>Restaurants</h1>
      <AppSelect @change="(e) => { selection = e }" />
    </div>
    <AppRestaurantInfo :selected="foodRestaurants" />
  </main>
</template>

<script>
import AppRestaurantInfo from '@/components/AppRestaurantInfo.vue'
import AppSelect from '@/components/AppSelect.vue'
import { mapState } from 'vuex'
export default {
  components: {
    AppRestaurantInfo,
    AppSelect
  },
  data () {
    return {
      selection: ''
    }
  },
  computed: {
    ...mapState(['fooddata']),
    foodRestaurants () {
      if (this.selection) {
        return this.fooddata.filter((f) => {
          const restaurant = f.name.toLowerCase()

          return restaurant.includes(this.selection)
        })
      }
      return this.fooddata
    }
  }

}
</script>

<style lang="scss" scoped>

</style>
