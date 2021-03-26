<template>
  <section class="restaurantinfo">
    <div v-for="restaurant in selected" :key="restaurant.id">
      <h2>{{ restaurant.name }}</h2>
      <p>Delivery Time : {{ restaurant.deliveryTime }}</p>
      <p>Rating : {{ restaurant.rating }}</p>
      <p v-if="restaurant.freeDelivery" class="label">
        <span>Free Delivery</span>
      </p>
      <div class="row">
        <div v-for="menuitem in restaurant.menu" :key="menuitem.id" class="items" :style="`background: url(${menuitem.img}) no-repeat  center center`">
          <div class="iteminfo">
            <div>
              <h4>{{ menuitem.item }}</h4>
              <p>{{ priceFormatting(menuitem.price) }}</p>
            </div>
            <nuxt-link :to="`/items/${menuitem.id}`" class="ghost">
              Order
            </nuxt-link>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import { mapState } from 'vuex'
export default {
  props: {
    // eslint-disable-next-line vue/require-default-prop
    selected: {
      type: [Array, Object]
    }
  },
  computed: {
    ...mapState(['fooddata'])
  },
  methods: {
    priceFormatting (item) {
      return '$' + item.toFixed(2)
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
