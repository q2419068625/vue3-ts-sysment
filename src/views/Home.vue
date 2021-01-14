<template>
  <div class="home container">
    <Alert v-if="alert" :message="alert" />
    <input type="text" class="form-control" placeholder="search..." v-model="filterInput">
    <table class="table table-striped">
      <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">姓名</th>
          <th scope="col">电话</th>
          <th scope="col">邮箱</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in filterBy(customers, filterInput)" :key="item.id">
          <th scope="row">{{ item.id }}</th>
          <td>{{ item.name }}</td>
          <td>{{ item.phone }}</td>
          <td>{{ item.email }}</td>
          <td>
             <router-link class="btn btn-warning" :to="'/details/' + item.id">详情</router-link>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, reactive, ref, toRefs } from "vue";
import axios from "axios";
import { Customer } from "@/utils/typs.ts";
import Alert from '@/components/Alert.vue';
import { useRoute } from 'vue-router'
export default defineComponent({
  name: "Home",
  setup() {
    const state = reactive({
      customers:<Customer[]> [],
      alert: <String> "",
      filterInput: <String> ""
    });
    const route = useRoute();

    if(route.query.alert){
      state.alert = String(route.query.alert);
      setTimeout(()=>{
        state.alert = ""
      },2000)
    }

    //发起请求
    onMounted(async () => {
      const res = await axios.get("http://localhost:3000/users");
      // console.log(res.data);
      state.customers = res.data;
    });

    //在现有的数据进行过滤
    function filterBy(customers: Customer[], value: string) {
        return customers.filter((customer: Customer) => {
          return customer.name.match(value)
          console.log(customer.name.match(value));
          
        })
    }
    

    return { ...toRefs(state), filterBy};
  },
  components: {Alert},
});
</script>
