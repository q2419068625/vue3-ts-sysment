<template>
  <div class="details container">
    <h1 class="page-header">
      <router-link class="btn btn-success" to="/">返回</router-link>
      <span style="float: right">
        <router-link class="btn btn-primary" to="/edit/1">编辑</router-link>
        &nbsp;
        <button class="btn  btn-danger">删除</button>
      </span>
    </h1>
  </div>
</template>

<script lang="ts">
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";
import axios from "axios";
import { Customer } from "@/utils/typs.ts";
export default {
  setup() {
    const route = useRoute();
    const customer = ref<Customer>();
    onMounted(async () => {
      const res = await axios.get(
        "http://localhost:3000/users/" + route.params.id
      );
      console.log(res.data);
      customer.value = res.data;
    });

    return { customer };
  },
};
</script>

<style scoped></style>
