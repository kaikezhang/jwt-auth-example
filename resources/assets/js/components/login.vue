<template>
  <div class="">
    <div class="alert alert-danger" v-if="error">
        <p>There was an error, unable to sign in with those credentials.</p>
    </div>
    <form autocomplete="off" v-on:submit.prevent="login">
        <div class="form-group">
            <label for="email">E-mail</label>
            <input type="email" id="email" class="form-control" placeholder="email" v-model="email" required>
        </div>
        <div class="form-group">
            <label for="password">Password</label>
            <input type="password" id="password" class="form-control" v-model="password" required>
        </div>
        <button type="submit" class="btn btn-default">Sign in</button>
    </form>
  </div>
</template>
<script>

export default {
    data() {
            return {
                email: null,
                password: null,
                error: false
            }
        },
        methods: {
            login(event) {
              let crediential = {
                email: this.email,
                password: this.password
              }

              window.axios.post('/auth/login', crediential)
                .then( response => {
                  console.log(response);
                  localStorage.setItem('id_token', response.headers.authorization);
                  this.$router.push('/');
                })
                .catch( error => {
                  console.log(error);
                  this.error= true;
                });
            }
        }
}
</script>
