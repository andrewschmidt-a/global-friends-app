<page>
    <actionBar title="Svelte Native App" />
    {#if !auth.loggedIn}
    <button on:tap={onTap}>Login</button>
    {/if}
    {#if auth.loggedIn}
    Loading...
    {/if}
</page>

<script>
    import Events from './Events.svelte'
    import { navigate } from 'svelte-native'

    function showAppWithProps() {
      navigate({
        page: Events,
        props: { firebase: firebase, auth: auth }
      })
    }
    let firebase = require("nativescript-plugin-firebase");

    let auth = {
      loggedIn: false,
      user: {}
    }
    
    firebase.init({
      // Optionally pass in properties for database, authentication and cloud messaging,
      // see their respective docs.
    }).then(
        function () {
          console.log("firebase.init done");
          
          console.log(firebaseWebApi.auth())
        },
        function (error) {
          console.log("firebase.init error: " + error);
        }
    );

    let logout = () => {
      auth.loggedIn = false
    }

    let onTap = ()=> {
      firebase.login({
            type: firebase.LoginType.FACEBOOK,
            // Optional
            facebookOptions: {
              // defaults to ['public_profile', 'email']
              scopes: ['public_profile', 'email'] // note: this property was renamed from "scope" in 8.4.0
            }
          }).then(
      function (result) {
        auth.user = result;
        auth.loggedIn = true;
        showAppWithProps()
      },
      function (errorMessage) {
        console.log("error:",errorMessage);
      }
  );
    }
</script>

<style>
    .info .fas {
        color: #3A53FF;
    }
    .info {
        font-size: 20;
    }
</style>
