<template>
  <div>
    <h1>Show All Pets</h1>
    <h2>จํานวนสัตว์เลี้ยงทั้งหมด {{ pets.length }} ตัว</h2>
    <div>
      <button @click="navigateTo('/pet/create')">+Create Pet</button>
      <button @click="navigateTo('/users')">กลับไป Users</button>
    </div>
    <hr />
    <div v-for="pet in pets" v-bind:key="pet.id">
      <p>Pet id : {{ pet.id }}</p>
      <p>ชื่อสัตว์เลี้ยง : {{ pet.name }}</p>
      <p>ประเภทสัตว์ : {{ pet.type }}</p>
      <p>สายพันธุ์ : {{ pet.species }}</p>
      <p>สีลำตัว : {{ pet.color }}</p>
      <p>ราคา : {{ pet.price }} บาท</p>
      <div>
        <button v-on:click="navigateTo('/pet/' + pet.id)">ดูข้อมูล Pet</button>
        <button @click="navigateTo('/pet/edit/' + pet.id)">Edit Pet</button>
        <button @click="deletePet(pet)">Delete Pet</button>
      </div>
      <hr />
    </div>
  </div>
</template>
<script>
import PetService from "@/services/PetService";

export default {
  data() {
    return {
      pets: []
    };
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deletePet(pet) {
      let result = confirm("Want of delete?");
      if (result) {
        try {
          await PetService.delete(pet);
          this.refreshData();
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this.pets = (await PetService.index()).data;
    }
  },
  async created() {
    try {
      this.pets = (await PetService.index()).data;
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style></style>
