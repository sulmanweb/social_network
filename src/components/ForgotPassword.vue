<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6 col-md-offset-3">
        <div class="jumbotron">
          <h2 class="text-center">Forgot Password?</h2>
          <form>
            <div class="alert alert-danger" role="alert" v-for="error in errors"
                 :key="error">{{ error }}
            </div>
            <div class="form-group">
              <label for="forgot-email" class="sr-only">Email*</label>
              <input type="text" class="form-control input-lg"
                     id="forgot-email" placeholder="Email*" required name="email"
                     v-model="form_data.email">
            </div>
            <button type="submit" class="btn btn-default btn-lg btn-block"
                    @click.prevent="submitForgot">
              <i class="fas fa-sync-alt"></i> Request Reset Password
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import HTTP from '../http_common';

  export default {
    name: 'ForgotPassword',
    data() {
      return {
        form_data: {},
        com_name: 'ForgotPassword',
        errors: [],
      };
    },
    methods: {
      submitForgot() {
        HTTP.post('/auth/reset_password', this.form_data)
          .then((response) => {
            // Show toast for success
            this.$toasted.show(response.data.message, {
              icon: 'check-circle',
              action: {
                text: 'CLOSE',
                onClick: (e, toastObject) => {
                  toastObject.goAway(0);
                },
              },
            });
            // Redirect to home component
            this.$router.push({name: 'Home'});
          })
          .catch((e) => {
            this.errors = e.response.data.errors;
          });
      },
    },
  };
</script>
