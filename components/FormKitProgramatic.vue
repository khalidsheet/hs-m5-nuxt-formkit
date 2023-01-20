<script setup>
const what = (value) => {
  console.log(value);
};

const yourSchemaArray = [
  {
    $el: "h1",
    attrs: {
      class: "text-4xl mb-4",
    },
    children: "Register",
  },
  {
    $formkit: "text",
    name: "email",
    label: "Email",
    help: "This will be used for your account.",
    validation: "required|email",
  },
  {
    $formkit: "password",
    name: "password",
    label: "Password",
    help: "Enter your new password.",
    validation: "required|length:5,16",
  },
  {
    $formkit: "password",
    name: "password_confirm",
    label: "Confirm password",
    help: "Enter your new password again to confirm it.",
    validation: "required|confirm",
    validationLabel: "password confirmation",
  },
  {
    $cmp: "FormKit",
    props: {
      name: "eu_citizen",
      type: "checkbox",
      id: "eu",
      label: "Are you a european citizen?",
    },
  },
  {
    $formkit: "select",
    if: "$get(eu).value", // 👀 Oooo, conditionals!
    name: "cookie_notice",
    label: "Cookie notice frequency",
    options: {
      refresh: "Every page load",
      hourly: "Ever hour",
      daily: "Every day",
    },
    help: "How often should we display a cookie notice?",
  },
];
</script>

<template>
  <div
    class="bg-gray-200 text-gray-900 h-screen flex items-center justify-center"
  >
    <div class="w-50">
      <FormKit type="form" @submit="what">
        <FormKitSchema :schema="yourSchemaArray" />
      </FormKit>
    </div>
  </div>
</template>
