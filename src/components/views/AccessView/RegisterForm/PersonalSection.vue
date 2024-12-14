<script setup lang="ts">
import Button from "@src/components/ui/inputs/Button.vue";
import LabeledTextInput from "@src/components/ui/inputs/LabeledTextInput.vue";
import { ref } from "vue";
import defaults from "@src/store/defaults";
import useStore from "@src/store/store";

const emit = defineEmits(['active-section-change'])
const firstName = ref('');
const lastName = ref('')
const userEmail = ref('')
// const store = useStore()

const emailValueChanged = (value: string) => {
  userEmail.value = value
}
const firstNameValueChanged = (value: string) => {
  firstName.value = value
}
const lastNameValueChanged = (value: string) => {
  lastName.value = value
}

const setPersonalInfo = () => {
  // set personal info in store
  defaults.user.firstName = firstName.value
  defaults.user.lastName = lastName.value
  defaults.user.email = userEmail.value
  // alert('first name:' + store.user?.firstName + " last name: " + store.user?.lastName)
  emit('active-section-change', {
    sectionName: 'password-section',
    animationName: 'slide-left',
  })

}

</script>

<template>
  <div>
    <!--form-->
    <div class="mb-5">
      <LabeledTextInput
        label="Email"
        placeholder="Enter your email"
        class="mb-5"
        @value-changed="emailValueChanged"
      />
      <LabeledTextInput
        label="First Name"
        placeholder="Enter your first name"
        class="mb-5"
        @value-changed="firstNameValueChanged"
      />
      <LabeledTextInput
        label="Last Name"
        placeholder="Enter your last name"
        class="mb-5"
        @value-changed="lastNameValueChanged"
      />
    </div>

    <!--local controls-->
    <div class="mb-6">
      <Button
        class="contained-primary contained-text w-full mb-4"
        @click="setPersonalInfo"
        >Next</Button
      >
    </div>

    <!--divider-->
    <div class="mb-6 flex items-center">
      <span
        class="w-full border border-dashed border-gray-100 dark:border-gray-600 rounded-[.0625rem]"
      ></span>
      <p class="body-3 text-color px-4 text-opacity-75 font-light">or</p>
      <span
        class="w-full border border-dashed border-gray-100 dark:border-gray-600 rounded-[.0625rem]"
      ></span>
    </div>

    <!--oauth controls-->
    <Button class="outlined-primary outlined-text w-full mb-5">
      <span class="flex">
        <img
          src="@src/assets/vectors/google-logo.svg"
          class="mr-3"
          alt="google-logo"
        />
        Sign in with google
      </span>
    </Button>
  </div>
</template>
