<template>
    <div>
        <navbar-login></navbar-login>
        <br><br><br>
        <div class="row">
        <div class="container mt-5 col-sm-8">
          <table class="table">
          <thead class="thead-dark">
            <tr>
              <th scope="col">No</th>
              <th scope="col">Item Name</th>
              <th scope="col">Quantity</th>
              <th scope="col">Total Price</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(product, index) in dataCart" :key="index">
              <th class="align-middle">{{index+1}}</th>
              <td class="align-middle">
                {{product.Product.name}}
                <p> <b>Description :</b> </p>
                {{product.Product.description}}
              </td>
              <td class="align-middle"> {{product.quantity}} </td>
              <td class="align-middle">Rp. {{ product.totalprice.toLocaleString('id-ID') }}</td>
            </tr>
          </tbody>
        </table>
        </div>
        <div class="container mt-5 col-sm-3">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title"> <b>Thank You</b> </h5>
              <p class="card-text">Thank you for all your purchase, we hope we can get new order from you</p>
              <button class="btn -btn-danger btn-sm" v-on:click="shopMore()"> <u> Shop More </u></button>
            </div>
          </div>
        </div>
        </div>
    </div>
</template>

<script>
import { mapState } from 'vuex'
import NavbarLogin from '../components/NavbarLogin.vue'

export default {
  components: { NavbarLogin },
  name: 'History',
  data () {
    return {
      activity: 0
    }
  },
  methods: {
    fetchHistory () {
      this.$store.dispatch('fetchHistory')
    },
    shopMore () {
      this.$router.push('/')
    },
    cekStatus () {
      this.$store.dispatch('cekStatus')
    }
  },
  created () {
    this.fetchHistory()
    this.cekStatus()
    this.$store.dispatch('totalShop')
  },
  watch: {
    activity (payload) {
      if (this.activity === 1) {
        this.activity = 0
        this.fetchHistory()
      }
    }
  },
  computed: {
    ...mapState(['dataCart', 'totalList', 'status'])
  }
}
</script>

<style>

</style>
