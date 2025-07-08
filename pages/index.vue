<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-data-table
        :headers="headers"
        :items="customers"
        :items-per-page="10"
        class="elevation-1"
        :loading="loading"
        loading-text="Loading... Please wait"
      >
        <template v-slot:item.profilePicture="{ item }">
          <v-badge
            color="purple"
            overlap
            content="VIP"
            offset-x="10"
            offset-y="40"
            bordered
            v-if="item.isVip == true"
          >
            <v-avatar size="100">
              <v-img
                lazy-src="https://picsum.photos/id/11/10/6"
                :src="item.profilePicture"
              ></v-img>
            </v-avatar>
          </v-badge>
          <div v-else>
            <v-avatar size="100">
              <v-img
                lazy-src="https://picsum.photos/id/11/10/6"
                :src="item.profilePicture"
              ></v-img>
            </v-avatar>
          </div>
        </template>
         <template v-slot:item.actions="{ item }">
          <v-btn color="primary" @click="getCustomersDetails(item)"> View</v-btn>
         </template>
      </v-data-table>
 <template>
  <div class="text-center">
    <v-dialog
      v-model="customerDialog"
      width="500"
    >
      <v-card>
      <v-toolbar class="primary text-h6">
        <v-toolbar-title>
          Customer Details
        </v-toolbar-title>
      </v-toolbar>
        <v-card-text class="mt-5">
          <v-row>
            <v-col cols="12" md="4">
              <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  max-height="150"
  max-width="250"
  src="https://picsum.photos/id/11/500/300"
></v-img>
              </v-col>
              <v-col cols="12" md="6">
                 <v-list-item two-line>
      <v-list-item-content>
        <v-list-item-subtitle>Name</v-list-item-subtitle>
        <v-list-item-title>{{ name }}</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
     <v-list-item two-line>
      <v-list-item-content>
        <v-list-item-subtitle>Email</v-list-item-subtitle>
        <v-list-item-title>{{ email }}</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
     <v-list-item two-line>
      <v-list-item-content>
        <v-list-item-subtitle>Phone</v-list-item-subtitle>
        <v-list-item-title>{{ phone }}</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
    <v-list-item two-line>
      <v-list-item-content>
        <v-list-item-subtitle>Age</v-list-item-subtitle>
        <v-list-item-title>{{ age }}</v-list-item-title>
      </v-list-item-content>
    </v-list-item>
              </v-col>
          </v-row>
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            color="primary"
            text
            @click="customerDialog = false"
          >
            I accept
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      headers: [
        // {
        //   text: 'ID',
        //   align: 'start',
        //   sortable: false,
        //   value: 'id',
        // },
        { text: "Photo", value: "profilePicture" },
        { text: "Name", value: "name" },
        { text: "Email", value: "email" },
        { text: "Phone", value: "phone" },
        { text: "Address", value: "address" },
        { text: "Age", value: "age" },
        { text: "Status", value: "isVip" },
        { text: "", value: "actions" },
      ],
      customers: [],
      name: "",
      email: "",
      phone: "",
      photo: "",
      age: 0,
      loading: true,
      customerDialog: false,
      
    };
  },
  methods: {
    getCustomers() {
      this.$axios
        .get("/customers")
        .then((response) => {
          console.log(response.data);
          this.customers = response.data;
          this.loading = false;
          
        })
        .catch((err) => {
          console.log(err);
        });
    },

    getCustomersDetails(item){
      console.log(item)
      this.name = item.name
      this.email = item.email
      this.phone = item.phone
      this.age = item.age
      this.customerDialog = true

    }
  },
  

  mounted() {
    this.getCustomers();
  },
};
</script>
