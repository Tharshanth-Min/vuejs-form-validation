<template>
  <div style="margin-top: 30px">
    <form @submit.prevent="onSubmit" class="register-form" novalidate="true">
      <h3 style="text-align: center">Add a user</h3>
      <label for="firstName">First name</label>
      <input id="firstName" v-model="firstName" />
      <ShowError v-if="errors.firstName" :errorText="errors.firstName" />

      <label for="lastName">Last name</label>
      <input id="lastName" v-model="lastName" />
      <ShowError v-if="errors.lastName" :errorText="errors.lastName" />

      <label for="email">Email</label>
      <input id="email" type="email" v-model="email" />

      <ShowError v-if="errors.email" :errorText="errors.email" />

      <input type="submit" class="button" value="Submit" />
    </form>
  </div>
</template>

<script>
import ShowError from "./ShowError.vue";

export default {
  name: "Form",
  components: {
    ShowError,
  },
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      users: [],
      errors: {},
    };
  },
  methods: {
    onSubmit() {
      let user = {
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
      };

      if (
        user.firstName &&
        user.lastName &&
        user.email &&
        this.validEmail(this.email)
      ) {
        alert(
          `Hello ${
            this.firstName + " " + this.lastName
          }! You have been registered successfully and the verification link has been sent to your email "${
            this.email
          }"`
        );
        if (window.confirm) {
          this.addUser(user);
          this.clearForm();
        }
        return;
      }
      if (!this.firstName) {
        this.errors["firstName"] = "First name required";
      } else {
        this.errors["firstName"] = null;
      }

      if (!this.lastName) {
        this.errors["lastName"] = "Last name required";
      } else {
        this.errors["lastName"] = null;
      }

      if (!this.email) {
        this.errors["email"] = "Email name required";
      } else if (!this.validEmail(this.email)) {
        this.errors["email"] = "Invalid email";
      } else {
        this.errors["email"] = null;
      }
    },
    addUser(user) {
      this.users.push(user);
    },
    clearForm() {
      this.firstName = "";
      this.lastName = "";
      this.email = "";
      this.errors = {};
    },
    validEmail: function (email) {
      var re =
        /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
  },
};
</script>

