<template>
  <article class="menu-item">
    <section
      class="div1"
      :style="`background: url(/${currentItem.img}) no-repeat center center`"
    />
    <section class="div2">
      <h2>{{ currentItem.item }}</h2>
      <p>Price: {{ currentPrice(currentItem.price) }}</p>
      <div class="quantity">
        <input v-model="quantity" type="number">
        <button>Add to Cart - {{ updatedPrice }}</button>
      </div>
    </section>
    <section class="div4">
      <h2>Description</h2>
      <p>{{ currentItem.description }}</p>
    </section>
    <section class="div3">
      <div v-if="currentItem.options">
        <fieldset>
          <legend><h3>options</h3></legend>
          <div v-for="item in currentItem.options" :key="item">
            <input :id="item" v-model="option" type="radio" name="option" :value="item">
            <label :for="item">{{ item }}</label>
            <br>
          </div>
        </fieldset>
      </div>
      <div v-if="currentItem.addOns">
        <fieldset>
          <legend><h3>add-ons</h3></legend>
          <div v-for="(item, index) in currentItem.addOns" :key="index">
            <input :id="item" v-model="addons" :value="item" type="checkbox" name="addon">
            <label :for="item">{{ item }}</label>
            <br>
          </div>
        </fieldset>
      </div>
    </section>
  </article>
</template>

<script>
import { mapState } from 'vuex'

export default {
  data () {
    return {
      id: this.$route.params.id,
      quantity: 0,
      option: '',
      addons: []
    }
  },
  computed: {
    ...mapState([
      'fooddata'
    ]),
    currentItem () {
      let result

      for (let i = 0; i < this.fooddata.length; i++) {
        for (let j = 0; j < this.fooddata[i].menu.length; j++) {
          if (this.fooddata[i].menu[j].id === this.id) {
            result = this.fooddata[i].menu[j]
            break
          }
        }
      }

      return result
    },
    updatedPrice () {
      return '$' + (this.quantity * this.currentItem.price).toFixed(2)
    }
  },
  methods: {
    currentPrice: (price) => {
      return '$' + price.toFixed(2)
    }
  }
}
</script>

<style lang="scss" scoped>
  .menu-item {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(5, 1fr);
    grid-column-gap: 20px;
    grid-row-gap: 20px;
    width: 1080px;
    margin: 5% auto;
  }
  .div1 { grid-area: 1 / 1 / 4 / 2; }
  .div2 { grid-area: 1 / 2 / 3 / 3; }
  .div3 { grid-area: 3 / 2 / 6 / 3; }
  .div4 { grid-area: 4 / 1 / 6 / 2; }

  .quantity {
    display: flex;
  }

  input[type=number] {
    width: 100px;
    font-size: large;
    padding: 12px;
  }
</style>
