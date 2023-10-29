<template>
  <div>
 <h1>Show Pet By Id</h1>
 <p>Pet id : {{ pet.id }}</p>
    <p>ชื่อสัตว์เลี้ยง : {{ pet.name }}</p>
      <p>ประเภทสัตว์ : {{ pet.type }}</p>
      <p>สายพันธุ์ : {{ pet.species }}</p>
      <p>ถิ่นกำเนิด : {{ pet.origin }}</p>
      <p>สีลำตัว : {{ pet.color }}</p>
      <p>น้ำหนัก : {{ pet.weight }} กิโลกรัม</p>
      <p>อุปนิสัย : {{ pet.character }}</p>
      <p>ราคา : {{ pet.price }} บาท</p>
 <div><button @click="navigateTo('/pet/edit/'+pet.id)">Edit Pet</button>
 <button @click="navigateTo('/pets')">กลับ</button></div>
  </div>
 </template>
 <script>
import PetService from "@/services/PetService";

export default {
  data() {
    return {
      pet: null
    };
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    }
  },
  async created() {
    try {
      let petId = this.$route.params.petId;
      this.pet = (await PetService.show(petId)).data;
      console.log(this.pet);
    } catch (err) {
      console.log(err);
    }
  }
};
</script>

<style></style>