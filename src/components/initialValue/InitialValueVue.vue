<script setup lang="ts">
import { useField, useForm } from 'vee-validate';
import { z } from 'zod';
import { toTypedSchema } from '@vee-validate/zod';

const validateSchema = z.object({
    username: z
        .string()
        .min(1, { message: 'Ce champ est obligatoire' })
        .min(3, { message: 'Ce est trop court' })
        .max(25, { message: 'Ce champ ne peut exéder 25 caractères' }),
});

useForm({
    validationSchema: toTypedSchema(validateSchema),
    initialValues: {
        username: 'Demo',
    },
});

const {
    value: usernameValue,
    errorMessage: usernameErrorMessage,
    handleChange,
} = useField('username', toTypedSchema(validateSchema), {
    validateOnValueUpdate: false,
});
</script>

<template>
    <fieldset>
        <legend>Initial value</legend>
        <label for="initialName">Nom</label>
        <input
            @blur="handleChange"
            v-model="usernameValue"
            type="text"
            id="initialName"
        />
        <br />
        <p v-if="usernameErrorMessage">{{ usernameErrorMessage }}</p>
        <p v-else>{{ usernameValue }}</p>
    </fieldset>
</template>

<style scoped lang="scss"></style>
