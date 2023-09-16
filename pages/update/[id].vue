<script setup>
import { useUserStore } from "~/stores/user";

const userStore = useUserStore();
const route = useRoute();
const router = useRouter();

const { data: job } = await useFetch(
  `http://127.0.0.1:8000/api/v1/jobs/${route.params.id}/`
);

console.log(job, "here edit job");

// const selectedCategory = ref("");
const title = ref(job.value.title);
const description = ref(job.value.description);
const position_salary = ref(job.value.position_salary);
const position_location = ref(job.value.position_location);
const company_name = ref(job.value.company_name);
const company_location = ref(job.value.company_location);
const company_email = ref(job.value.company_email);
const errors = ref([]);

onMounted(() => {
  if (!userStore.user.isAuthenticated) {
    router.push("/auth/login");
  }
});

const updateForm = async () => {
  await $fetch(
    `http://127.0.0.1:8000/api/v1/jobs/update-job/${route.params.id}/`,
    {
      method: "PUT",
      headers: {
        Authorization: "token " + userStore.user.token,
        "Content-Type": "application/json",
      },
      body: {
        category: job.value.category,
        title: title.value,
        description: description.value,
        position_salary: position_salary.value,
        position_location: position_location.value,
        company_name: company_name.value,
        company_location: company_location.value,
        company_email: company_email.value,
      },
    }
  )
    .then((response) => {
      router.push("/myjobs");
    })
    .catch((error) => {
      if (error.response) {
        for (const property in error.response._data) {
          errors.value.push(`${property}: ${error.response._data[property]}`);
        }
      } else if (error.message) {
        errors.value.push("Something went wrong. Please try again.");
      }
    });
};
</script>
<template>
  <div class="px-6 py-10">
    <h1 class="text-3xl font-bold">Update job!</h1>

    <form @submit.prevent="updateForm" class="space-y-4">
      <!-- <div>
        <label>Category</label>

        <select
          class="appearance-none px-4 h-10 md:!h-[50px] w-full border border-black outline-none bg-white rounded-md"
          id="selectedSubscription"
          name="SelectedSubscription"
          v-model="selectedCategory"
        >
          <option
            v-for="(option, index) in jobCategories"
            :key="index"
            :value="option.id"
          >
            {{ option.title }}
          </option>
        </select>
      </div> -->

      <div>
        <label>Title</label>
        <input
          v-model="title"
          type="text"
          class="w-1/2 mt-2 p-4 rounded-xl bg-gray-100"
        />
      </div>

      <div>
        <label>Description</label>
        <textarea
          v-model="description"
          class="w-1/2 mt-2 p-4 rounded-xl bg-gray-100"
        />
      </div>

      <div>
        <label>Salary</label>
        <input
          v-model="position_salary"
          type="text"
          class="w-1/2 mt-2 p-4 rounded-xl bg-gray-100"
        />
      </div>

      <div>
        <label>Location</label>
        <input
          v-model="position_location"
          type="text"
          class="w-1/2 mt-2 p-4 rounded-xl bg-gray-100"
        />
      </div>

      <div>
        <label>Company name</label>
        <input
          v-model="company_name"
          type="text"
          class="w-1/2 mt-2 p-4 rounded-xl bg-gray-100"
        />
      </div>

      <div>
        <label>Company location</label>
        <input
          v-model="company_location"
          type="text"
          class="w-1/2 mt-2 p-4 rounded-xl bg-gray-100"
        />
      </div>

      <div>
        <label>Company e-mail</label>
        <input
          v-model="company_email"
          type="text"
          class="w-1/2 mt-2 p-4 rounded-xl bg-gray-100"
        />
      </div>

      <div></div>

      <div
        v-if="errors.length"
        class="mb-6 py-4 px-6 bg-rose-400 text-white rounded-lg"
      >
        <p v-for="error in errors" :key="error">
          {{ error }}
        </p>
      </div>

      <div class="text-white">
        <button class="p-3 bg-slate-800 rounded-lg">Save Changes</button>
      </div>
    </form>
  </div>
</template>

<style lang="scss" scoped></style>
