<template>
  <div
    class=" border border-white 
    border-2 shadow-lg 
    bg-white
    font-semibold m-2 
    rounded-xl p-2 h-min"
  >
  <div class="text-center my-3 underline text-amber-700"> Input Details of the package </div>
    <!-- Client Name -->
    <div class="m-2 text-left text-xs">
      <span class="text-amber-700  "> Client Name: {{ message }}</span>
      <input
        v-model.lazy="clientName"
        class="px-2 border border-2 p-1 mx-2 rounded-lg"
        placeholder="Mr/Mrs Name"
      />
    </div>

    <!-- client Phone Number -->
    <div class="m-2 py-1 text-left text-xs">
      <span class="text-amber-700 ">Client PhoneNumber: </span>
      <input
        v-model.lazy="clientContacts"
        class="px-2 border 
         border-2 p-1 mx-2 rounded-lg"
        placeholder="0712345678"
      />
    </div>

    <!-- Client Location -->
    <div class="m-2 p-1 text-left text-xs">
      <span class="text-amber-700  ">Drop Location: </span>
      <input
        v-model.lazy="dropLocation"
        class="px-2 border 
          border-2 p-1 
        mx-2 rounded-lg"
        placeholder=" eg. Madaraka Shopping centre, house 19"
      />
    </div>

    <!-- Special Instructions -->
    <div class="m-2 p-1 text-left text-xs">
      <span class="text-amber-700 ">Special Instructions:</span>
      <input
        v-model.lazy="specialInstructions"
        class="px-2 border 
         border-2
         mx-2 p-1 rounded-lg"
        placeholder=" eg don't mention sender's name "
      />
    </div>

    <!-- PAckage Label  -->
    <div class="m-2 p-1 text-left text-xs">
      <span class="text-amber-700">How have you labelled the Package ? </span>
      <input
        v-model.lazy.trim="packageLabel"
        class="px-2 border
           border-2
          p-1 mx-2 rounded-lg"
        placeholder=" eg. package for Jimmy Hendrix"
      />
    </div>

    <div>
      <button
        @click="addNewOrder()"
        class="py-2 px-7 m-3 rounded-3xl bg-white
         font-bold uppercase border border-amber-200 
         hover:border-amber-700 text-xs
         text-amber-700
          transition hover:-translate-y-0.5 hover:shadow-xl rounded"
      >
        Add Delivery
      </button>
    </div>
      <div v-if="addDeliveryClicked === true" class="transition ease-in-out delay-300
       bg-orange-100 border-l-4 rounded border-orange-500 text-orange-700 p-4" role="alert">
  <p class="font-bold">Success</p>
  <p>Item SuccessFully added.</p>

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
      addDeliveryClicked:false
    };
  },
  methods: {
    addNewOrder() { 
        this.addDeliveryClicked = true
      this.sendFirebaseData(
        this.clientName,
        this.clientContacts,
        this.dropLocation,
        this.specialInstructions,
        this.packageLabel
      ); 
      setTimeout(() => {  this.addDeliveryClicked = false}, 1000);
     
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
    //    this.addDeliveryClicked = false
    },
  },
  mounted() {},
};
</script>

<style></style>
