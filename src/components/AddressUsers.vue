<template>
  <div class="address_users">
    <AddButton @addNewAddress="addNewAddress" :ad="updateAd" />
    <div class="all_address">
      <div class="header_">
        <span class="item">ID</span>
        <span class="item">Address</span>
        <span class="item">Labels</span>
        <span class="item">By Name</span>
        <span class="item">Phone</span>
      </div>
      <Address
        v-for="adres in address"
        :key="adres"
        :id="adres.id"
        :location="adres.location"
        :place="adres.place"
        :labels="adres.labels"
        :proper="adres.propert"
        :phone="adres.phone"
        @update="updateAddress"
      />
    </div>
  </div>
</template>

<script>
import AddButton from "@/components/AddButton";
import Address from "@/components/Address";
export default {
  name: "AddressUsers",
  components: { Address, AddButton },
  data: function () {
    return {
      address: [
        {
          id: 1,
          location: "CAMEROON",
          place: "DOUALA-BONABERI",
          phone: "06 77 75 48 14",
          propert: "Brice MONTHE DJEUMOU",
          labels: ["Friends"],
          family: "xvbdfgb",
          street_address: "Mélen, Yaoundé",
          postal_code: 8172,
          email: "monthedjeumoubrice2000@gmail.com",
        },
      ],
      updateAd: null,
    };
  },
  methods: {
    addNewAddress(newAddress) {
      const size = this.address.length;
      this.address.push({ id: size + 1, ...newAddress });
      window.localStorage.clear();
      window.localStorage.setItem("address", JSON.stringify(this.address));
    },
    updateAddress(id) {
      this.updateAd = this.address.find((item) => item.id === id);
      console.log(id);
      console.log(this.updateAd, typeof this.updateAd);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
