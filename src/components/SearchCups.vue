<template>
  <form @submit.prevent="onSubmit">
    <input type="text" v-model="title" placeholder="Enter your CUPS" />
    <button type="submit" name="submit" class="secondary">
      search
    </button>
  </form>
  <div class="grid">
    <ClientInfo :client="client" />
    <Offer :offer="offer" />
  </div>
</template>

<script>
import ClientInfo from '@/components/ClientInfo.vue';
import Offer from '@/components/Offer.vue'
import supplyPoints from "@/api/supply-points";

export default {
  props: ["clients"],
  data() {
    return {
      title: "",
      client: "",
      offer: "",
      allNeighbors: [],
      power: {}
    };
  },
  methods: {
    onSubmit() {
      this.clients.forEach(client => {
        if (this.title.trim() && this.title == client.cups) {
          return this.client = client;
        }
      });
      this.title = "";
      this.addOffer(this.client);
    },

    addOffer(client) {
      const offerStandart = "Standard offer: No discount, no conditions."
      const offerBasic = "Basic discount: 5% discount."
      const offerSpecial = "Special discount: 12% discount."
      supplyPoints.forEach(supply_point => {
        if (client.building_type === "house" && client.cups === supply_point.cups && supply_point.neighbors.length > 1) {
          return (this.allNeighbors = supply_point.neighbors,
            this.power = supply_point.power)
        }
      })
      this.sumInvoces(this.allNeighbors, this.power, supplyPoints, offerSpecial, offerBasic, offerStandart)
    },
    sumInvoces(neighbors, power, supplyPoints, offerSpecial, offerBasic, offerStandart) {
      let sum = 0;
      let sumP1 = 0;
      let sumP2 = 0
      neighbors.length > 1 ?
        (neighbors.forEach(neighbor => {
          supplyPoints.forEach(supply_point => {
            if (supply_point.cups === neighbor) {
              sum += Number(supply_point.invoiced_amount)
              sumP1 += Number(supply_point.power.p1)
              sumP2 += Number(supply_point.power.p2)
              if (sum > 100) {
                return this.offer = offerSpecial
              } else if (sumP1 < power.p1 && sumP2 < power.p2) {
                return this.offer = offerBasic
              } else {
                return this.offer = offerStandart
              }
            }
          })
        })) : null
    }
  },
  components: { ClientInfo, Offer }
}
</script>

<style>

</style>
