<template>
  <div class="details container">
    <h1 class="page-header">
      <router-link class="btn btn-success" to="/">返回</router-link>
      <span style="float: right">
        <router-link class="btn btn-primary" to="/edit/1">编辑</router-link>
        &nbsp;
        <button class="btn  btn-danger" @click="deleteCustomer">删除</button>
      </span>
    </h1>

    <ul class="list-group">
        <li class="list-group-item">
            <i class="fa fa-user" aria-hidden="true"></i>
            {{customer.name}}
        </li>
        <li class="list-group-item">
            <i class="fa fa-mobile" aria-hidden="true"></i>
            {{customer.phone}}
        </li>
        <li class="list-group-item">
            <i class="fa fa-envelope-open" aria-hidden="true"></i>
            {{customer.email}}
        </li>
        <li class="list-group-item">
            <i class="fa fa-superpowers" aria-hidden="true"></i>
            {{customer.education}}
        </li>
        <li class="list-group-item">
            <i class="fa fa-bandcamp" aria-hidden="true"></i>
            {{customer.graduationschool}}
        </li>
        <li class="list-group-item">
            <i class="fa fa-meetup" aria-hidden="true"></i>
            {{customer.profession}}
        </li>
        <li class="list-group-item">
            <i class="fa fa-wpexplorer" aria-hidden="true"></i>
            {{customer.profile}}
        </li>
    </ul>
  </div>
</template>

<script lang="ts">
import { onMounted, ref } from "vue";
import { useRoute, useRouter } from "vue-router";
import axios from "axios";
import { Customer } from "@/utils/typs.ts";
export default {
  setup() {
    const route = useRoute();
    const router = useRouter();
    const customer = ref<Object>({});
    onMounted(async () => {
      const res = await axios.get(
        "http://localhost:3000/users/" + route.params.id
      );
      console.log(res.data);
      customer.value = res.data;
    });
    //删除
    async function deleteCustomer() {
        const res = await axios.delete(
        "http://localhost:3000/users/" + route.params.id
      );
      router.push("/")
    }

    return { customer, deleteCustomer };
  },
};
</script>

<style scoped></style>
