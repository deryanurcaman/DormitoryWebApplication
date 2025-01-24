<template>
<!-- frontend part for the share news page -->
  <app-layout title="Dashboard">
    <template #header>
      <h2 class="font-semibold text-xl text-gray-800 leading-tight">
        Share Announcements
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <form class="space-y-8 divide-y divide-gray-200">
          <div class="space-y-8 divide-y divide-gray-200 sm:space-y-5">
            <div class="flex flex-col">
              <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                <div
                  class="
                    py-2
                    align-middle
                    inline-block
                    min-w-full
                    sm:px-6
                    lg:px-8
                  "
                >
                  <div class="overflow-hidden sm:rounded-lg">
                    <form
                      @submit="submit"
                      class="space-y-8 divide-y divide-gray-200"
                    >
                      <div class="space-y-8 divide-y divide-gray-200">
                        <div>
                          <div>
                            <h3
                              class="
                                text-lg
                                leading-6
                                font-medium
                                text-gray-900
                              "
                            >
                              Add A New Announcement
                            </h3>
                            <p class="mt-1 text-sm text-gray-500">
                              You can add a new announcement here.
                            </p>
                          </div>

                          <div
                            class="
                              mt-6
                              grid grid-cols-1
                              gap-y-6 gap-x-4
                              sm:grid-cols-6
                            "
                          >
                            <div class="sm:col-span-4">
                              <label
                                for="title"
                                class="block text-sm font-medium text-gray-700"
                              >
                                Title
                              </label>
                              <div class="mt-1 flex rounded-md shadow-sm">
                                <input
                                  required
                                  v-model="form.title"
                                  type="text"
                                  name="title"
                                  id="title"
                                  autocomplete="title"
                                  class="
                                    flex-1
                                    focus:ring-indigo-500
                                    focus:border-indigo-500
                                    block
                                    w-full
                                    min-w-0
                                    rounded-none rounded-r-md
                                    sm:text-sm
                                    border-gray-300
                                    text-gray-700
                                  "
                                />
                              </div>
                            </div>
                            

                            <div class="sm:col-span-6">
                              <label
                                for="description"
                                class="block text-sm font-medium text-gray-700"
                              >
                                Description
                              </label>
                              <div class="mt-1">
                                <textarea
                                  required
                                  v-model="form.description"
                                  id="description"
                                  name="description"
                                  rows="3"
                                  class="
                                    shadow-sm
                                    focus:ring-indigo-500
                                    focus:border-indigo-500
                                    block
                                    w-full
                                    sm:text-sm
                                    border border-gray-300
                                    rounded-md
                                    text-gray-700
                                  "
                                />
                              </div>
                            </div>
                          </div>
                        </div>
                      </div>

                      <div class="pt-5">
                        <div class="flex justify-end">
                          <jet-button
                            wire:click.prevent="store()"
                            class="ml-4"
                            :class="{ 'opacity-25': form.processing }"
                            :disabled="form.processing"
                          >
                            Share
                          </jet-button>
                        </div>
                      </div>
                    </form>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </form>
      </div>
    </div>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <h1 class="text-lg leading-6 font-medium text-gray-900">All Announcements</h1>
        <p class="mt-1 text-sm text-gray-500 mb-4">
          You can see all announcements here.
        </p>
        <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
          <ul
            role="list"
            class="
              grid grid-cols-1
              gap-6
              sm:grid-cols-2
              md:grid-cols-3
              lg:grid-cols-4
            "
          >
            <li
              v-for="person in news"
              :key="person.title"
              class="
                col-span-1
                flex flex-col
                text-center
                bg-white
                rounded-lg
                shadow
                divide-y divide-gray-200
              "
            >
              <div class="flex-1 flex flex-col p-8">
                <img
                  class="w-32 h-32 flex-shrink-0 mx-auto rounded-full"
                  src="https://d338t8kmirgyke.cloudfront.net/icons/icon_pngs/000/013/421/original/announcement_4585245.png"
                  alt=""
                />
                <h2 class="mt-6 text-gray-900 text-xl font-medium">
                  {{ person.title }}
                </h2>
                <dl class="mt-1 flex-grow flex flex-col justify-between">
                  <dt class="sr-only">Title</dt>
                  <dd class="text-gray-500 text-sm">
                    {{ person.description }}
                  </dd>
                  <dt class="sr-only">Role</dt>
                  <dd class="mt-3">
                    <span
                      class="
                        px-2
                        py-1
                        text-green-800 text-xs
                        font-medium
                        bg-green-100
                        rounded-full
                      "
                      >{{ moment(person.created_at).format("MMMM Do YYYY, h:mm a") }}</span
                    >
                  </dd>
                  <dt class="sr-only">Role</dt>
                  <dd class="mt-3">
                    <jet-button
                      @click="deleteRow(person)"
                      :class="{ 'opacity-25': form.processing }"
                      :disabled="form.processing"
                    >
                      Delete
                    </jet-button>
                  </dd>
                </dl>
              </div>
              <div></div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </app-layout>
</template>

<script>
//javascript part for the share news
import { defineComponent } from "vue";
import AppLayout from "@/Layouts/AppLayout.vue";
import Welcome from "@/Jetstream/Welcome.vue";
import "@themesberg/flowbite";
import { Head, Link } from "@inertiajs/inertia-vue3";
import JetButton from "@/Jetstream/Button.vue";
import moment from "moment";


export default defineComponent({
  props: ["news"],
  components: {
    Head,
    Link,
    AppLayout,
    Welcome,
    JetButton,
  },
  data() {
    return {
      editMode: false,
      isOpen: false,
      form: this.$inertia.form({
        title: "",
        description: "",
      }),
      moment: moment
    };
  },
  methods: {
    submit() {
      this.form.post(this.route("news.store"));
      this.reset();
    },
    deleteRow: function (data) {
      if (!confirm("Are you sure want to remove?")) return;
      data._method = "DELETE";
      this.$inertia.post("/news/" + data.id, data);
      this.reset();
    },
    reset: function () {
      this.form = {
        title: null,
        description: null,
      };
    },
  },
});
</script>
