<template>
  <nav>
    <ul>
      <li>
        <nuxt-link exact to="/">
          Home
        </nuxt-link>
      </li>
      <li>
        <!-- Do not forget '/' in links or the paths will be computed in relation to last visited path and leads to undefined data-->
        <nuxt-link to="/restaurants">
          Restaurants
        </nuxt-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {

}
</script>

<style lang="scss" scoped>
  a {
    margin-right: 12px;
  }
</style>
