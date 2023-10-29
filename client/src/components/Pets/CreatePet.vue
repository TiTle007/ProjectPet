<template>
  <div>
    <h1>Create Pet</h1>
    <form v-on:submit.prevent="createPet">
      <p>ชื่อสัตว์เลี้ยง : <input type="text" v-model="pet.name" /></p>
      <p>ประเภทสัตว์ : <input type="text" v-model="pet.type" /></p>
      <p>สายพันธุ์ : <input type="text" v-model="pet.species" /></p>
      <p>ถิ่นกำเนิด : <input type="text" v-model="pet.origin" /></p>
      <p>สีลำตัว : <input type="text" v-model="pet.color" /></p>
      <p>น้ำหนัก : <input type="text" v-model="pet.weight" /> กิโลกรัม</p>
      <p>อุปนิสัย : <input type="text" v-model="pet.character" /></p>
      <p>ราคา : <input type="text" v-model="pet.price" /> บาท</p>
      <p><button type="submit">Create Pet</button></p>
    </form>
  </div>
</template>
<script>
import PetService from "@/services/PetService";
export default {
  data() {
    return {
      pet: {
        name: "",
        type: "",
        species: "",
        origin: "",
        color: "",
        weight: "",
        character: "",
        price: ""
      }
    };
  },
  methods: {
    async createPet() {
      try {
        await PetService.post(this.pet);
        this.$router.push({
          name: "pets"
        });
      } catch (err) {
        console.log(err);
      }
    }
  }
};
</script>
<style scoped></style>
