<script setup>
import "@formkit/themes/genesis";
import { useQRCode } from "@vueuse/integrations/useQRCode";

let isAllGood = ref(false);
let qr = ref(null);

const submitForm = (data) => {
  qr = useQRCode(JSON.stringify(data));
  isAllGood.value = true;
  console.log(qr);
};
</script>

<template>
  <div
    class="bg-gray-200 text-gray-900 h-screen flex items-center justify-center"
  >
    <div class="w-50">
      <FormKit
        v-if="!isAllGood"
        type="form"
        @submit="submitForm"
        submit-label="HEey"
        :actions="false"
      >
        <FormKit type="group" name="address">
          <FormKit
            name="firstname"
            type="text"
            label="First Name"
            :validation="[['required']]"
            :validation-messages="{
              required: `What should we call you?`,
            }"
          />
          <FormKit
            name="lastname"
            type="text"
            label="Last Name"
            :validation="[['required']]"
            :validation-messages="{
              required: `What should we call you?`,
            }"
          />
        </FormKit>
        <FormKit
          name="username"
          type="text"
          prefixIcon="user"
          label="Username"
          help="usernames must be between 3 and 15"
          :validation="[['required']]"
          :validation-messages="{
            required: `You know what? Usernames are amazing, choose one :)`,
          }"
        />

        <FormKit
          name="password"
          type="password"
          label="Password"
          :validation="[['required']]"
          :validation-messages="{
            required: `Yooo, what is your password? huh!`,
          }"
        />
        <FormKit
          name="re_password"
          type="password"
          label="Password"
          :validation="[['required'], ['confirm', 'password']]"
          :validation-messages="{
            required: `Hey, just making sure you are not coping & pasting the password ;)`,
          }"
        />
        <FormKit
          type="url"
          name="url"
          label="Website"
          placeholder="https://www.example.com..."
          validation="url"
          help="Do you have a website?"
        />
        <!-- <FormKit
          type="file"
          label="Documents"
          help="Upload as many verifications documents as you can, it will help you with your case."
          multiple="true"
          accept=".pdf"
        /> -->
        <FormKit type="submit" />
      </FormKit>
      <div v-else class="flex justify-center items-center flex-col space-y-10">
        <div class="text-2xl">Cool! Here's your QR Code</div>
        <img :src="qr" alt="" />
        <div class="text-muted">
          You can use this QR to validate your appointment
        </div>
        <div>
          <button
            class="py-4 bg-gray-400 px-16 rounded text-xl"
            @click="isAllGood = false"
          >
            Back
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
