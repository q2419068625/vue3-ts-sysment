<template>
  <div class="home container">
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
        <tr v-for="item in customers" :key="item.id">
          <th scope="row">{{ item.id }}</th>
          <td>{{ item.name }}</td>
          <td>{{ item.phone }}</td>
          <td>{{ item.email }}</td>
          <td></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, reactive, ref, toRefs } from "vue";
import axios from "axios";
export default defineComponent({
  name: "Home",
  setup() {
    const state = reactive({
      customers: [],
    });

    //发起请求
    onMounted(async () => {
      const res = await axios.get("http://localhost:3000/users");
      console.log(res.data);
      state.customers = res.data;
    });

    return { ...toRefs(state) };
  },
  components: {},
});
</script>
