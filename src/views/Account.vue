<template>
  <div class="account">
    <div class="pageHeader">
      <h1 class="center">Welcome!</h1>
    </div>
    <div class="formContent">
      <div v-if="!accountCreated || showForm">
        <p>Please create a new account by filling out the information below:</p>
        <form @submit.prevent="createAccount">
          <input type="text" v-model="name" placeholder="Name">
          <p></p>
          <input type="text" v-model="email" placeholder="Email">
          <p></p>
          <div id="checkboxes">
            <p id="dietary_restrictions">Check your dietary attributes:</p>
            <input type="checkbox" class="checkbox-button" v-model="glutenFree" id="glutenFree">
              <label for="glutenFree">Gluten-free</label><br>
            <input type="checkbox" class="checkbox-button" v-model="dairyFree" id="dairyFree">
              <label for="dairyFree">Dairy-free</label><br>
            <input type="checkbox" class="checkbox-button" v-model="nutFree" id="nutFree">
              <label for="nutFree">Nut free</label><br>
            <input type="checkbox" class="checkbox-button" v-model="vegan" id="vegan">
              <label for="vegan">Vegan</label><br>
          </div>
          <br />
          <button type="submit">Save</button>
        </form>

      </div>
      <div v-else class="center">
        <h3>Hello {{accountName}}!</h3>
        <p>{{accountEmail}}</p>
        <br />
        <div v-if="dairyFree || nutFree || vegan || glutenFree">
          <h4>Dietary attributes:</h4>
          <p v-if="dairyFree">Dairy Free</p>
          <p v-if="nutFree">Nut Free</p>
          <p v-if="vegan">Vegan</p>
          <p></p>
          <p v-if="glutenFree" id="gluten-free-message">We see you are Gluten Free! Everything in our bakery is gluten free so you 
            can choose anything off the menu and be reassured it is safe :)</p>
        </div>
        <div v-else>
          <p>No dietary restrictions</p>
        </div>
        <p id="edit-button"><a @click="toggleForm">Edit your account</a></p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Account',
  data() {
    return {
      name: "",
      email: "",
      glutenFree: false,
      /*dairyFree: false,
      nutFree: false,
      vegan: false,*/
      showForm: false
    }
  },
  computed: {
    accountCreated() {
      return (this.$root.$data.account.name !== "");
    },
    account() {
      return this.$root.$data.account;
    },
    accountName() {
      return this.$root.$data.account.name;
    },
    accountEmail() {
      return this.$root.$data.account.email;
    },
    dairyFree: {
      get: function() {
        return this.$root.$data.account.allergyAttributes.dairyFree;
      },
      set: function(newValue) {
        this.$root.$data.account.allergyAttributes.dairyFree = newValue;
      }
    },
    nutFree: {
      get: function() {
        return this.$root.$data.account.allergyAttributes.nutFree;
      },
      set: function(newValue) {
        this.$root.$data.account.allergyAttributes.nutFree = newValue;
      }
    },
    vegan: {
      get: function() {
        return this.$root.$data.account.allergyAttributes.vegan;
      },
      set: function(newValue) {
        this.$root.$data.account.allergyAttributes.vegan = newValue;
      }
    },
    accountAllergyAttributes() {
      return this.$root.$data.account.allergyAttributes;
    }
  },
  methods: {
    createAccount() {
      this.$root.$data.account.name = this.name;
      this.$root.$data.account.email = this.email;
      this.$root.$data.account.allergyAttributes.dairyFree = this.dairyFree;
      this.$root.$data.account.allergyAttributes.nutFree = this.nutFree;
      this.$root.$data.account.allergyAttributes.vegan = this.vegan;
      this.showForm = false;
    },
    toggleForm() {
      this.showForm = !this.showForm;
    }
  }
}
</script>

<style scoped>
.formContent {
  padding-left: 100px;
  padding-right: 100px;
  margin-top: 100px;
  margin-bottom: 400px;
}
.center {
  width: 100%;
}
input {
  padding: 10px;
  border:0;
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
  border-radius:10px;
}
input[type=text] {
  width: 50%;
}
input[type=checkbox] {
  margin-top: 10px;
  margin-bottom: 10px;
  margin-left: 20px;
}
#checkboxes {
  margin-top: 30px;
}
button {
  background-color: #3F5957;
  border: none;
  color: white;
  padding: 5px 10px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 12px;
  margin: 4px 2px;
  cursor: pointer;
}
button:hover {
  background-color: #73908F;
}
#gluten-free-message {
  color: #3F5957;
  font-style: italic;
  margin-top: 30px;
}
#edit-button {
  margin-top: 30px;
  color: grey;
}
#edit-button:hover {
  color: black;
  cursor: pointer;
}
@media screen and (min-width: 800px) {
  .formContent {
    padding-left: 300px;
    padding-right: 300px;
  }
}
</style>