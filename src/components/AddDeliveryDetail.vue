<template>
  <div
    class="w-1/2 border border-red-100 border-4 font-semibold m-2 rounded-xl p-2"
  >
    <!-- Client Name -->
    <div class="m-2 text-left text-xs">
      <span class="  "> Client Name: {{ message }}</span>
      <input
        v-model.lazy="clientName"
        class="px-2 border border-red-100 border-2 p-1 mx-2 rounded"
        placeholder="Mr/Mrs Name"
      />
    </div>

    <!-- client Phone Number -->
    <div class="m-2 py-1 text-left text-xs">
      <span>Client PhoneNumber: </span>
      <input
        v-model.lazy="clientContacts"
        class="px-2 border border-red-100 border-2 p-1 mx-2 rounded"
        placeholder="0712345678"
      />
    </div>

    <!-- Client Location -->
    <div class="m-2 p-1 text-left text-xs">
      <span>Drop Location: </span>
      <input
        v-model.lazy="dropLocation"
        class="px-2 border border-red-100 border-2 p-1 mx-2 rounded"
        placeholder=" eg. Madaraka Shopping centre, house 19"
      />
    </div>

    <!-- Special Instructions -->
    <div class="m-2 p-1 text-left text-xs">
      <span>Special Instructions:</span>
      <input
        v-model.lazy="specialInstructions"
        class="px-2 border border-red-100 border-2 mx-2 p-1 rounded"
        placeholder=" eg don't mention sender's name "
      />
    </div>

    <!-- PAckage Label  -->
    <div class="m-2 p-1 text-left text-xs">
      <span>How have you labelled the Package ? </span>
      <input
        v-model.lazy.trim="packageLabel"
        class="px-2 border border-red-100 border-2 p-1 mx-2 rounded"
        placeholder=" eg. package for Jimmy Hendrix"
      />
    </div>

    <div>
      <button
        @click="addNewOrder()"
        class="py-2 px-7 m-3 rounded-3xl font-bold uppercase border border-red-100 text-xs transition hover:-translate-y-0.5 hover:shadow-xl rounded"
      >
        Add Delivery
      </button>
    </div>
  </div>
</template>

<script>
import { getDatabase, ref, push } from "firebase/database";

export default {
  data() {
    return {
      clientName: "",
      clientContacts: "",
      dropLocation: "",
      specialInstructions: "",
      packageLabel: "",
    };
  },
  methods: {
    addNewOrder() {
      console.log("= ", this.clientName);
      console.log("= ", this.clientContacts);
      console.log("= ", this.specialInstructions);
      this.sendFirebaseData(
        this.clientName,
        this.clientContacts,
        this.dropLocation,
        this.specialInstructions,
        this.packageLabel
      );
    },

    sendFirebaseData(name, contact, location, instructions, labelid) {
      const db = getDatabase();
      push(ref(db, "deliveries"), {
        clientName: name,
        clientContact: contact,
        dropLocation: location,
        specialInstructions: instructions,
        label: labelid,
        status: "REQUESTED",
      });

      this.clientName = "";
      this.clientContacts = "";
      this.specialInstructions = "";
      this.specialInstructions = "";
      this.packageLabel = "";
    },
  },
  mounted() {},
};
</script>

<style></style>
