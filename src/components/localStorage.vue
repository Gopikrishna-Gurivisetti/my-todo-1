<template>
    <div class="mt-32 ms-24">
        <input class="border border-2 border-blue-400 rounded py-2 ps-3" type="text" v-model="newItem"
            placeholder="Enter user name...">
        <button class="ms-5 px-3 py-1 border border-2 border-blue-400 bg-green-300 rounded" @click="createItem">Add</button>

        <!-- print the data in tabular format -->
        <table>
            <th>
                <h1 class="text-3xl mt-5 mb-5 p-2 bg-blue-500 rounded text-white">User Details in Local Storage</h1>
            </th>
            <tr v-for="(item, index) in items" :key="index">
                <td class="py-3">
                    <input class="me-5" v-model="selectItem" type="checkbox" :value="index" @click="checkedItem(index)" />
                    <span class="text-red-600 text-2xl">{{ item }}</span>
                </td>
                <td><button class="mx-10 px-3 py-1 border border-2 border-green-400 bg-orange-300 rounded"
                        @click="updateItem(index)">Update</button></td>
                <td><button class="mx-10 px-3 py-1 border border-2 border-blue-400 bg-red-400 rounded"
                        @click="deleteItem(index)">Delete</button></td>
            </tr>
        </table>


        <table>
            <th>
                <h1 class="text-3xl mt-5 mb-5 p-2 bg-purple-500 rounded text-white">User Details in Session Storage</h1>
            </th>
            <tr v-for="(data, index) in sessionItem" :key="index">
                <td class="py-3">
                    <!-- <input class="me-5" v-model="selectItem" type="checkbox" :value="index" @click="checkedItem(index)" /> -->
                    <span class="text-red-600 text-2xl">{{ data }}</span>
                </td>
                <!-- <td><button class="mx-10 px-3 py-1 border border-2 border-green-400 bg-orange-300 rounded"
                        @click="updateItem(index)">Update</button></td>
                <td><button class="mx-10 px-3 py-1 border border-2 border-blue-400 bg-red-400 rounded"
                        @click="deleteItem(index)">Delete</button></td> -->
            </tr>
        </table>


    </div>
</template>
  
<script setup>
import { ref } from 'vue';

const items = ref([]);
const newItem = ref('')
const selectItem = ref(false);
const sessionItem = ref([]);

// Read the array from local storage when the component is mounted
const arrayString = localStorage.getItem('myArrayKey');
items.value = JSON.parse(arrayString) || [];

const sessionString = sessionStorage.getItem('mysessionKey');
sessionItem.value = JSON.parse(sessionString) || [];


function createItem() {
    // Create - Add a new item to the array
    if (newItem.value.trim() !== "") {
        items.value.push(newItem.value);
        newItem.value = '';
    }

    // Write the updated array back to local storage
    updateLocalStorage();
}

function updateItem(index) {
    // Update - Modify an item in the array
    const updatedValue = prompt('Enter the updated value:');
    if (updatedValue) {
        items.value[index] = updatedValue;

        // Write the updated array back to local storage
        updateLocalStorage();
    }
}

function deleteItem(index) {
    // Delete - Remove an item from the array
    items.value.splice(index, 1);

    // Write the updated array back to local storage
    updateLocalStorage();
}
const updateLocalStorage = () => {
    // Write the updated array to local storage
    localStorage.setItem('myArrayKey', JSON.stringify(items.value));
}

function checkedItem(index) {
    let waitItem = items.value.splice(index, 1);
    waitItem.forEach(item => {
        sessionItem.value.push(item);
    })

    console.log(waitItem);
    updateLocalStorage();
    sessionStorage.setItem('mysessionKey', JSON.stringify(sessionItem.value));
}


</script>
  