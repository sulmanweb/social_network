<template>
  <div class="container">
    <h1 class="text-center">Social Casts</h1>
    <div class="row">
      <div class="col-md-8 col-md-offset-2">
        <form>
          <div class="alert alert-danger" role="alert" v-for="error in errors"
               :key="error">{{ error }}
          </div>
          <div class="form-group">
            <label for="new-post-home" class="sr-only">New Post</label>
            <textarea class="form-control input-lg" id="new-post-home" placeholder="New Post..." required
                      name="new-post-home" v-model="new_post_form_data.body" rows="3"></textarea>
          </div>
          <button type="submit" class="btn btn-default btn-lg btn-block"
                  @click.prevent="submitNewPost">
            <i class="fas fa-pencil-alt"></i> Post It!
          </button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
  import HTTP from '../http_common';

  export default {
    name: 'Home',
    data() {
      return {
        com_name: 'Home',
        isLoggedIn: false,
        errors: [],
        new_post_form_data: {},
      };
    },
    methods: {},
    mounted() {
      this.isLoggedIn = localStorage.getItem('auth') !== null;
      if (!this.isLoggedIn) {
        this.$router.push({name: 'SignIn'});
      } //else do show homepage
    },
  };
</script>
