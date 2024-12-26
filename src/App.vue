<template>
  <div>
    <div v-if="loading" class="flex justify-center items-center h-screen">
        <img src="./assets/ZZ5H.gif" />
    </div>
    <div v-else-if="error" class="flex justify-center items-center h-screen">
      <p class="text-rose-600 text-2xl font-bold">{{ error }}</p>
    </div>
  <div class="px-8 bg-gray-100" v-else>
    <h1 class="text-4xl font-bold">Complex Buggy Component</h1>

    <Counter /> 
    <div>
      <h2 class="text-3xl font-bold mt-3">Data List</h2>
      <div class="grid md:grid-cols-4 grid-cols-2 gap-4 cursor-pointer">
        <div v-for="item in data" :key="item.id" @click="logItemId(item.id)" class="shadow p-2 rounded-md">
          <p class="font-bold capitalize">{{ item.title.length > 10 ? item.title.slice(0, 10) + '...' : item.title }}</p> 
        </div>
      </div>
    </div>

    <div class="mt-10 pb-5">
      <h2 class="text-3xl font-bold mt-3">Filtered Data</h2>
      <div class="grid md:grid-cols-4 grid-cols-2 gap-4 cursor-pointer">
      <div v-for="item in filteredData" :key="item.id" @click="logItemId(item.id)" class="shadow p-2 rounded-md">
        <p class="font-bold capitalize"> 
            {{ item.title }}
        </p>
      </div>
    </div>
    </div>
  </div>

</div>

  <Modal :singleUser="singleUser" v-if="showModal" @close="showModal = false" />

  <!-- Task List: 
1: Counter Fix
2 : If "Record" is clicked, show the specific record.
3 : Fix any bugs found and resolve them. -->
</template>

<script>
import { ref, computed, onMounted } from 'vue';
import Modal from './components/Modal.vue';
import Counter from './components/Counter.vue';

export default {
  components: {
      Modal,
      Counter
  },
  setup() {
    const data = ref([]);
    const loading = ref(false);
    const error = ref(null);
    const singleUser = ref(null);
    const showModal = ref(false);

    const fetchDataFromAPI = async () => {
      try {
        loading.value = true;
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        const json = await response.json();
        data.value = json;
      } catch (err) {
        error.value = err.message;
      } finally {
        loading.value = false;     
      }
    };

    onMounted(() => {
      loading.value = false;
       fetchDataFromAPI();
    });

    const filteredData = computed(() => {
      return data.value.filter((item) => item.userId === 1);
    });

    const logItemId = (id) => {
      console.log(id);
      singleUser.value = data.value.filter(el => el.id ===id)[0];
      showModal.value = true;
    };


    return {
      data,
      loading,
      error,
      filteredData,
      logItemId,
      singleUser,
      showModal
    };
  },
};
</script>

