<template>
  <FormikForm :initialValues="values" :validate="validate" @onSubmit="onSubmit">
      <FormikField name="name" type="text" placeholder="Name" />
      <p v-if="errors.name">{{ errors.name }}</p>
      <FormikField name="email" type="email" placeholder="Email" />
      <p v-if="errors.email">{{ errors.email }}</p>
      <FormikField name="password" type="password" placeholder="Password" />
      <p v-if="errors.password">{{ errors.password }}</p>
      <button type="submit" :disabled="isSubmitting">Submit</button>
  </FormikForm>
</template>

<script setup>
  import FormikField from "./components/FormikField.vue";
  import FormikForm from "./components/FormikForm.vue";

  const values = {
    name: "",
    email: "",
    password: "",
  };

  const validate = (values) => {
    const errors = {};

    if (!values.name) {
      errors.name = "Name is required";
    }

    if (!values.email) {
      errors.email = "Email is required";
    } else if (
      !/^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}$/i.test(values.email)
    ) {
      errors.email = "Invalid email address";
    }

    if (!values.password) {
      errors.password = "Password is required";
    }

    return errors;
  };

</script>