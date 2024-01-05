<script setup lang="ts">
import { useField, useForm } from 'vee-validate';

// useForm
const validationSchema = {
    username(value?: string): boolean | string {
        if (!value || !value.length) {
            return 'Le champ est obligatoire';
        } else if (value.length < 3) {
            return 'trop court !';
        } else if (value.length > 10) {
            return 'trop long !!';
        } else {
            return true;
        }
    },
    email(value?: string): boolean | string {
        if (value.includes('@') && value.length > 5) {
            return true;
        } else {
            return "L'email est invalide";
        }
    },
};

useForm({
    validationSchema,
});

const { value: emailValue, errorMessage: emailErrorMessage } =
    useField('email');
const { value: usernameValue, errorMessage: usernameErrorMessage } =
    useField('username');
console.log({
    username: { usernameValue, usernameErrorMessage },
    email: { emailValue, emailErrorMessage },
});
</script>

<template>
    <p>useField doit être invoqué impérativement APRES useForm</p>
    <fieldset>
        <legend>usernameValue</legend>
        <label for="username">Nom</label>&nbsp;
        <input type="text" v-model="usernameValue" />
        <br />
        <label for="email">email</label>&nbsp;
        <input type="email" v-model="emailValue" />
        <h3>Result</h3>
        <p v-if="usernameErrorMessage">{{ usernameErrorMessage }}</p>
        <p>{{ usernameValue }}</p>
        <p v-if="emailErrorMessage">{{ emailErrorMessage }}</p>
        <p>{{ emailValue }}</p>
    </fieldset>
</template>

<style scoped lang="scss"></style>
