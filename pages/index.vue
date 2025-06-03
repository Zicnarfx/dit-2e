<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="" md="">
     <template>
  <v-data-table
    :headers="headers"
    :items="customers"
    :items-per-page="10"
    class="elevation-1"
    :loading="loading"
    loading-text="Loading Please Wait"


  >
<template v-slot:item.profilePicture="{ item}">

  <v-badge
  color="purple"
  content="VIP"
  offset-x="110"
  offset-y="15"
  bordered
  v-if="item.isVip == true"
  >
  <v-avatar size="100">

 <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  max-height="100"
  max-width="100"
  :src='item.profilePicture'

></v-img>
</v-avatar>
</v-badge>

<div v-else>
  
  <v-avatar size="100">
 <v-img
  lazy-src="https://picsum.photos/id/11/10/6"
  max-height="100"
  max-width="100"
  :src='item.profilePicture'

></v-img>
</v-avatar>
</div>
</template>

</v-data-table>
</template>
    </v-col>
  </v-row>
</template>

<script>
import { colors } from 'vuetify/lib'

export default {
  name: 'IndexPage',
  data () {
    return {
       headers: [
          // {
          //   text: 'ID',
          //   align: 'start',
          //   sortable: false,
          //   value: 'id',
          // },
          { text: 'Photo', value: 'profilePicture' },
          { text: 'Name', value: 'name' },
          { text: 'Enail', value: 'email' },
          { text: 'Phone', value: 'phone' },
          { text: 'Address', value: 'address' },
          { text: 'Age', value: 'age' },
          { text: 'Status', value: 'isVip' },
        ],
        customers: [

        ],
        loading: true
    } 
  }, 

  methods: {
    getCustomers(){
      this.$axios.get('/customers')
      .then(response => {
        console.log (response.data)
        this.customers = response.data
        this.loading = false
      })
      .catch(err => {
        console.log(err)
      })
    }
  },

  mounted() {
    this.getCustomers()
  }

}
</script>
