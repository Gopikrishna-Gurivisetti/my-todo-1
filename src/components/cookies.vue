
  <template>
    <div class="mt-10">
      <button class="px-5 py-2 rounded border border-2 bg-red-300 mx-5" @click="setCookie">Set Cookie</button>
      <button class="px-5 py-2 rounded border border-2 bg-red-300 mx-5" @click="changeExpiryTime">Change Expiry Time</button>
      <button class="px-5 py-2 rounded border border-2 bg-red-300 mx-5" @click="getCookie">Get Cookie</button>
      <button class="px-5 py-2 rounded border border-2 bg-red-300 mx-5" @click="deleteCookie">Delete Cookie</button>
    </div>
  </template>
  
  <script setup>
  import {ref} from "vue";
  import Cookies from 'js-cookie';
  
 const name =ref('Hello, world!')
   
     function setCookie() {
        // Set a cookie with an expiry time of 1 hour (3600 seconds)
        const expiryInSeconds = 2;
        const expiryDate =  new Date(Date.now() + expiryInSeconds * 1000);
        Cookies.set('myCookie', name.value, { expires: expiryDate });
      }

      function changeExpiryTime() {
        // Change the expiry time of the cookie to 30 minutes (1800 seconds) from the current time
        const currentCookieValue = Cookies.get('myCookie');
        if (currentCookieValue) {
          const expiryInSeconds = 5;
          const expiryDate =  new Date(Date.now() + expiryInSeconds * 1000);
          Cookies.set('myCookie', currentCookieValue, { expires: expiryDate });
        }
      }

      function getCookie() {
        const cookieValue = Cookies.get('myCookie');
        console.log(cookieValue);
      }

      function deleteCookie() {
        Cookies.remove('myCookie');
      }
    

  </script>