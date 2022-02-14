<template>
  <div
    class="  text-left m-3 p-3 border border-gray-300 bg-white border-1 shadow-lg rounded-lg  "
    v-for="data in clientOrders"
    :key="data.id"
  >
    <div class="text-base ">
      Package : <span class="  text-gray-500">{{ data.label }}</span>
     
     <div class="flex float-right my-2 shadow rounded-lg">
          <span
        v-if="data.status === 'REQUESTED'"
        class=" text-xs text-center font-bold px-2 py-1.5   w-24  bg-blue-700 text-white rounded-lg"
      >
        {{ data.status }}</span
      >
      <span
        v-if="data.status === 'STARTED'"
        class="  text-xs font-bold text-center px-2 py-1.5   w-24 bg-orange-500 text-white  rounded-lg"
      >
        {{ data.status }}</span
      >
      <span
        v-if="data.status === 'DELIVERED'"
        class="  text-xs px-2 font-bold text-center  py-1.5 w-24  bg-green-500 text-white  rounded-lg"
      >
        {{ data.status }}</span
      >  
     </div>
  
    </div>
    <div class="mx-3 text-xs   m-1">
      Client Name : <span class="  text-gray-500"> {{ data.clientName }}</span>
    </div>
    <div class="mx-3 text-xs m-1 ">
      Client Contact : <span class="  text-gray-500">{{ data.clientContact }}</span>
    </div>
    <div class="mx-3 text-xs m-1  font-light">
      Drop Location : <span class="font-normal text-gray-500"> {{ data.dropLocation }}</span>
    </div>
    <div class="mx-3 text-xs m-1">
      Special Instructions :
      <span class="font-normal text-gray-500">{{ data.specialInstructions }}</span>
    </div>
    <div>
      <button
        @click="removeThisOrder(data.id)"
        class="py-1 px-5 m-2 rounded-xl  
         font-bold uppercase border bg-red-700 text-white text-xs transition hover:-translate-y-0.5 hover:shadow-xl rounded"
      >
        Delete Item
      </button>
    </div>
      <div v-if="deleteDeliveryClicked === true" class="transition ease-in-out delay-300
       bg-red-100 border-l-4 rounded border-red-500 text-red-700 p-4" role="alert">
  <p class="font-bold">Success</p>
  <p>Item SuccessFully deleted.</p>
</div>
  </div>
</template>

<script>
import { getDatabase, ref, push, onValue , remove} from "firebase/database";
      const db = getDatabase();
export default {
  data() {
    return {
      clientName: "",
      clientContacts: "",
      dropLocation: "",
      specialInstructions: "",
      packageLabel: "",
      deliveryStatus: "",
      clientOrders: [],
      deleteDeliveryClicked:false
    };
  },
  methods: {
    getDataFromFRDB() {
      const deliveryCountRef = ref(db, "deliveries/");
      onValue(deliveryCountRef, (snapshot) => {
        const data = snapshot.val();
        const dataKey = snapshot.toJSON();
        let AllData = [];
        snapshot.forEach(function (childSnapshot) {
          //   console.log(", >>> ", childSnapshot.key);
          const data = childSnapshot.val(childSnapshot.key);
          let deleivery = {
            clientName: data.clientName,
            clientContact: data.clientContact,
            dropLocation: data.dropLocation,
            specialInstructions: data.specialInstructions,
            label: data.label,
            status: data.status,
            id:childSnapshot.key
          };
          //   console.log("DATA  = ", deleivery);
          AllData.push(deleivery);
        });
        this.clientOrders = AllData;
      });
    },
    removeThisOrder(id){
     console.log("id --- ", id)
     this.deleteDeliveryClicked = true
            setTimeout(() => {  this.deleteDeliveryClicked = false}, 1000);
     remove(ref(db, "deliveries/"+id));
    }
  },
  mounted() {
    this.getDataFromFRDB();
  },
};
</script>

<style></style>
