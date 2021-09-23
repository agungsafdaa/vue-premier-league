<template>
 <router-link :to="'/detail/'">
  <div class="card mb-10">
    <!-- <img
      class="card-img-top"
      :src="'assets/' + product.gambar"
      alt="Card image cap"
    /> -->
    <div class="card-body">
      <!-- <h5 class="mt-0">{{ products.competition.map((standing) => ` 
         <h6> ${competition.code}</h6>
         `).join('')}}</h5> -->
         <h3>{{standings.stage}}</h3>
      <!-- <p class="card-text">Harga : {{ product.harga || toCurrency }}</p> -->
      <router-link to="/" class="btn btn-sm btn-success"
        ><b-icon-cart></b-icon-cart>Pesan Sekarang</router-link
      >
    </div>
  </div>
  </router-link>
</template>

<script>
export default {
  Name: "CardProduct",
  props: ["product"],
};
// eslint-disable-next-line no-undef
</script>

<style>
</style>