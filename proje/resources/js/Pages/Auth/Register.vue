<template>
  <Head title="Register" />

  <jet-authentication-card>
    <p style="text-align: center"><b>REGISTER</b></p>
    <template #logo>
      <jet-authentication-card-logo />
    </template>

    <jet-validation-errors class="mb-4" />

    <form @submit.prevent="submit">
      <!-- <div>
        <fieldset class="mt-4">
          <div
            class="space-y-4 sm:flex sm:items-center sm:space-y-0 sm:space-x-10"
          >
            <div
              v-for="notificationMethod in notificationMethods"
              :key="notificationMethod.id"
              class="flex items-center"
            >
              <input
                :id="notificationMethod.id"
                name="notification-method"
                type="radio"
                :checked="notificationMethod.id === 'email'"
                class="
                  focus:ring-indigo-500
                  h-4
                  w-4
                  text-indigo-600
                  border-gray-300
                "
              />
              <label
                :for="notificationMethod.id"
                class="ml-3 block text-sm font-medium text-gray-700"
              >
                {{ notificationMethod.title }}
              </label>
            </div>
          </div>
        </fieldset>
      </div> -->
      <div class="mt-4">
        <jet-label for="role" value="Role" />
                <x-jet-label for="role" value="role" />
                <select id="role" name="role" required v-model="form.role" x-model="role" class="block mt-1 w-full text-gray-700 border-gray-300 focus:border-indigo-300 focus:ring focus:ring-indigo-200 focus:ring-opacity-50 rounded-md shadow-sm">
                    <option value="student">Student</option>
                    <option value="personnel">Personnel</option>
                </select>
            </div>
      <div class="mt-4">
        <jet-label for="name" value="Name" />
        <jet-input
          id="name"
          type="text"
          class="mt-1 block w-full text-gray-700"
          v-model="form.name"
          required
          autofocus
          autocomplete="name"
        />
      </div>

      <div class="mt-4">
        <jet-label for="surname" value="Surname" />
        <jet-input
          id="surname"
          type="text"
          class="mt-1 block w-full text-gray-700"
          v-model="form.surname"
          required
          autofocus
          autocomplete="surname"
        />
      </div>

      <div class="mt-4">
        <jet-label for="email" value="Email" />
        <jet-input
          id="email"
          type="email"
          class="mt-1 block w-full text-gray-700"
          v-model="form.email"
          required
        />
      </div>

      <div class="mt-4">
        <jet-label for="password" value="Password" />
        <jet-input
          id="password"
          type="password"
          class="mt-1 block w-full text-gray-700"
          v-model="form.password"
          required
          autocomplete="new-password"
        />
      </div>

      <div class="mt-4">
        <jet-label for="password_confirmation" value="Confirm Password" />
        <jet-input
          id="password_confirmation"
          type="password"
          class="mt-1 block w-full text-gray-700"
          v-model="form.password_confirmation"
          required
          autocomplete="new-password"
        />
      </div>

      <div
        class="mt-4"
        v-if="$page.props.jetstream.hasTermsAndPrivacyPolicyFeature"
      >
        <jet-label for="terms">
          <div class="flex items-center">
            <jet-checkbox
              name="terms"
              id="terms"
              v-model:checked="form.terms"
            />

            <div class="ml-2">
              I agree to the
              <a
                target="_blank"
                :href="route('terms.show')"
                class="underline text-sm text-gray-600 hover:text-gray-900"
                >Terms of Service</a
              >
              and
              <a
                target="_blank"
                :href="route('policy.show')"
                class="underline text-sm text-gray-600 hover:text-gray-900"
                >Privacy Policy</a
              >
            </div>
          </div>
        </jet-label>
      </div>

      <div class="flex items-center justify-end mt-4">
        <Link
          :href="route('login')"
          class="underline text-sm text-gray-600 hover:text-gray-900"
        >
          Already registered?
        </Link>

        <jet-button
          class="ml-4"
          :class="{ 'opacity-25': form.processing }"
          :disabled="form.processing"
        >
          Register
        </jet-button>
      </div>
    </form>
  </jet-authentication-card>
</template>

<script>
import { defineComponent } from "vue";
import JetAuthenticationCard from "@/Jetstream/AuthenticationCard.vue";
import JetAuthenticationCardLogo from "@/Jetstream/AuthenticationCardLogo.vue";
import JetButton from "@/Jetstream/Button.vue";
import JetInput from "@/Jetstream/Input.vue";
import JetCheckbox from "@/Jetstream/Checkbox.vue";
import JetLabel from "@/Jetstream/Label.vue";
import JetValidationErrors from "@/Jetstream/ValidationErrors.vue";
import { Head, Link } from "@inertiajs/inertia-vue3";

export default defineComponent({
  components: {
    Head,
    JetAuthenticationCard,
    JetAuthenticationCardLogo,
    JetButton,
    JetInput,
    JetCheckbox,
    JetLabel,
    JetValidationErrors,
    Link,
  },

  data() {
    return {
      form: this.$inertia.form({
        name: "",
        surname: "",
        email: "",
        role: "",
        password: "",
        password_confirmation: "",
        terms: false,
      }),
      notificationMethods,
    };
  },

  methods: {
    submit() {
      this.form.post(this.route("register"));
    },
  },
});
const notificationMethods = [
  { id: "student", title: "Student" },
  { id: "personnel", title: "Personnel" },
];
</script>

<style>
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  width: 50%;
}

p {
  font-size: 40px;
  color: rgb(97, 97, 163);
}
</style>