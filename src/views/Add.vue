<template>
  <div class="home container">
    <form @submit.prevent="addCustomer">
      <div class="form-group">
        <label for="exampleFormControlInput1">姓名</label>
        <input
          type="text"
          class="form-control"
          placeholder="name..."
          v-model="customer.name"
        />
      </div>
      <div class="form-group">
        <label for="exampleFormControlInput1">电话</label>
        <input
          type="text"
          class="form-control"
          placeholder="phone..."
          v-model="customer.phone"
        />
      </div>
      <div class="form-group">
        <label for="exampleFormControlInput1">邮箱</label>
        <input
          type="email"
          class="form-control"
          placeholder="email..."
          v-model="customer.email"
        />
      </div>
      <div class="form-group">
        <label for="exampleFormControlInput1">学历</label>
        <input
          type="text"
          class="form-control"
          placeholder="education..."
          v-model="customer.education"
        />
      </div>
      <div class="form-group">
        <label for="exampleFormControlInput1">毕业学校</label>
        <input
          type="text"
          class="form-control"
          placeholder="graduation school..."
          v-model="customer.graduationschool"
        />
      </div>
      <div class="form-group">
        <label for="exampleFormControlInput1">毕业学校</label>
        <input
          type="text"
          class="form-control"
          placeholder="profession..."
          v-model="customer.profession"
        />
      </div>

      <div class="form-group">
        <label for="exampleFormControlTextarea1">个人简介</label>
        <textarea
          class="form-control"
          v-model="customer.profile"
          rows="7"
        ></textarea>
      </div>
      <button type="submit" class="btn btn-primary btn-block">提交</button>
    </form>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, reactive, ref, toRefs } from "vue";
import axios from "axios";
import { Customer } from "@/utils/typs.ts";
export default defineComponent({
  name: "Add",
  setup() {
    const state = reactive({
      customer:<Customer>{
        name: "",
        phone: "",
        email: "",
        education: "",
        graduationschool: "",
        profession: "",
        profile: "",
      },
    });
     function addCustomer() {
         console.log(state.customer);
         
     }
    return {
        ...toRefs(state),
        addCustomer
    };
  },
  components: {},
});
</script>
