<template>
  <!--MAIN-->
  <main>
    <!--REGISTER ADDRESS-->
    <div class="registerAddress mt-3">
      <div class="container c-section">
        <div class="row">
          <div class="col-sm-2"></div>
          <div class="col-sm-10">
            <div class="a-section a-spacing-medium">
              <div class="a-subheader a-breadcrumb a-spacing-small">
                      <small>Your Account > </small>
                      <small>Your Adresses</small>
              </div>
              <h3 class="a-spacing-medium a-spacing-top-medium">Your Addresses</h3>
              <h6><a href="/hh/address/add"
                      style="text-decoration:none;"
                    >
                      Add Address
                    </a></h6>
              <!-- Message from Server -->
              <div class="a-section a-spacing-none a-spacing-top-small mt-2 text-muted">
                {{message}}
              </div>
              <br/>
              <div class="a-spacing-double-large mt-2">
                  <!-- Address -->
                  <div class="row row-cols-1 row-cols-md-3 mt-10">
                    <div class="col mb-4" v-for="(address, index) in addresses" :key="address._id">
                      <div class="card h-100 text-dark haha" style="border-width: 0; border-radius: 10px; background: none;">
                        <div class="a-box a-spacing-none normal-desktop-address-tile mt-2 pl-2">
                      <div class="a-box-inner a-padding-none">
                        <div class="address-section-no-default">
                          <div class="a-spacing-small">
                            <ul class="a-unordered-list a-nostyle a-vertical" style="list-style-type:none;">
                              <li>
                                <h5>
                                  <!-- Address Fullname -->
                                  <b>{{address.fullName}}</b>
                                </h5>
                              </li>
                              <!-- Address house number -->
                              <li>{{address.houseNumber}}</li>
                              <!-- Address street address -->
                              <li>{{address.streetAddress}}</li>
                              <!-- Address city state zip code -->
                              <li>{{address.city}}, {{address.state}}</li>
                              <!-- Address country -->
                              <li>{{address.country}}, {{address.pincode}}</li>
                              <!-- Address Phone number -->
                              <li>Phone number: {{address.phoneNumber}}</li>
                            </ul>
                          </div>
                        </div>
                      </div>
                      <!-- Update Button -->
                      <div class="edit-address-desktop-link">
                        <a :href="`/hh/address/${address._id}`">Edit</a>
                        &nbsp; | &nbsp;
                        <!-- Delete Button -->
                        <a href="#" @click="onDeleteAddress(address._id, index)">Delete</a>
                        &nbsp; | &nbsp;
                        <!-- Set Address as Default -->
                        <a href="#" @click="onSetDefault(address._id)">Set as Default</a>
                      </div>
                    </div>
                      </div>
                    </div>
                  </div>
              </div>
              

                  </div>
                </div>
              </div>
            </div>
          </div>
    <!--/REGISTER ADDRESS-->
  </main>
  <!--/MAIN-->
</template>

<script>
export default {
    async asyncData({$axios}){
        try{
            let response = await $axios.$get("/api/addresses");
            return {
                addresses: response.addresses
            }
        } catch(err){
            console.log(err);
        }
    },
    data() {
        return {
            message: ""
        }
    },
    methods: {
        async onDeleteAddress(id, index) {
             try{
                 let response = await this.$axios.$delete(`/api/addresses/${id}`);
                 if(response.success) {
                     this.message = response.message;
                     this.addresses.splice(index, 1);
                 }
             } catch(err){
                 this.message = err.message;
                 console.log(err);
             }
        },

        async onSetDefault(id) {
            try{
                let response = await this.$axios.$put(`api/addresses/set/default`, {id: id});

                 if(response.success) {
                     this.message = response.message;
                     await this.$auth.fetchUser();
                 }
            } catch(err){
                this.message = err.message;
                 console.log(err);
            }
        }
    }
}
</script>