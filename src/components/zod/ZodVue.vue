<script setup lang="ts">
import { useField, useForm } from 'vee-validate';
import { z } from 'zod';
import { toTypedSchema } from '@vee-validate/zod';

const validationSchema = z.object({
    useremail: z.string().email(),
    username: z
        .string()
        .min(1, { message: 'Obligatoire' })
        .min(3, { message: 'Trop court' })
        .max(10, { message: 'Trop long' }),
});

// A INITILISEZ EN PREMIER, DONC IMPERATIVEMENT AVANT "useForm"
useForm({
    validationSchema: toTypedSchema(validationSchema),
});

const { value: emailValue, errorMessage: emailErrorMessage } = useField(
    'useremail',
    toTypedSchema(validationSchema),
);
const { value: usernameValue, errorMessage: usernameErrorMessage } = useField(
    'username',
    toTypedSchema(validationSchema),
);
console.log({
    username: { usernameValue, usernameErrorMessage },
    useremail: { emailValue, emailErrorMessage },
});
</script>

<template>
    <ul>
        <li><a href="https://github.com/colinhacks/zod">lien github</a></li>
    </ul>
    <fieldset>
        <legend>Zod</legend>
        <label for="username">Nom</label>&nbsp;
        <input type="text" v-model="usernameValue" id="username" />
        <br />
        <label for="useremail">email</label>&nbsp;
        <input type="email" v-model="emailValue" id="useremail" />
        <h3>Result</h3>
        <p class="error" v-if="usernameErrorMessage">
            {{ usernameErrorMessage }}
        </p>
        <p>{{ usernameValue }}</p>
        <p class="error" v-if="emailErrorMessage">{{ emailErrorMessage }}</p>
        <p>{{ emailValue }}</p>
    </fieldset>
</template>

<style scoped lang="scss">
.error {
    color: crimson;
}
</style>
