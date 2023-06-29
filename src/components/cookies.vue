
  <!-- <template>
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
        const expiryInSeconds = 500;
        const expiryDate =  new Date(Date.now() + expiryInSeconds * 1000);
        Cookies.set('myCookie','Hello, world!', { expires: expiryDate });
      }

      function changeExpiryTime() {
        // Change the expiry time of the cookie to 30 minutes (1800 seconds) from the current time
        const currentCookieValue = Cookies.get('myCookie');
        if (currentCookieValue) {
          const expiryInSeconds = 700;
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
        console.log("Remove Cookie");
      }
    

  </script> -->

  <template>
    <div class="mt-10 ms-24">

      <table>
        <th>
          <h1 class="text-3xl mt-5 mb-5 p-2 bg-orange-500 rounded text-white">Cookies</h1>
        </th>
        <tr>
          <td><button class="px-5 py-2 rounded border border-2 bg-green-300 mx-5 border-blue-300"  @click="setCookie">Set Cookie</button></td>
          <td><button class="px-5 py-2 rounded border border-2 bg-orange-300 mx-5 border-blue-300"  @click="getCookie">Get Cookie</button></td>
          <td><button class="px-5 py-2 rounded border border-2 bg-red-300 mx-5 border-blue-300"  @click="deleteCookie">Delete Cookie</button></td>
        </tr>
      </table>
      
    </div>
  </template>
  
  <script setup>
 
  
   
     function setCookie() {
        const cookieName = 'myCookie';
        const cookieValue = 'Hello Cookies!!';
        const expiryDays = 1;
        const date = new Date();
        date.setTime(date.getTime() + expiryDays * 1 * 1 * 6 * 1000);
        const expires = `expires=${date.toUTCString()}`;
  
        document.cookie = `${cookieName}=${cookieValue};${expires};path=/`;
      }

     function getCookie() {
        const cookieName = 'myCookie';
        const name = `${cookieName}=`;
        const decodedCookie = decodeURIComponent(document.cookie);
        const cookieArray = decodedCookie.split(';');
  
        for (let i = 0; i < cookieArray.length; i++) {
          let cookie = cookieArray[i];
          while (cookie.charAt(0) === ' ') {
            cookie = cookie.substring(1);
          }
          if (cookie.indexOf(name) === 0) {
            const value = cookie.substring(name.length, cookie.length);
            console.log(value);
            return value;
          }
        }document
        return '';
      }

     function deleteCookie() {
        const cookieName = 'myCookie';
        document.cookie = `${cookieName}=;expires=Thu, 01 Jan 1970 00:00:00 UTC;path=/;`;
      }
   
 
  </script>