<template>
  <div class="content">
    <TitleMenu/>
    <AddressUsers/>
  </div>
</template>

<script>
import TitleMenu from "@/components/TitleMenu";
import AddressUsers from "@/components/AddressUsers";

export default {
  name: 'App',
  components: {
    TitleMenu,
    AddressUsers
  }
}
</script>

<style>

</style>
