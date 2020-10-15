<template>
<div>
    <h1>Hola, para poder ingresar debes iniciar sesion con tu cuenta Google</h1>
    <button @click="userSignIn">Iniciar sesion</button>
</div>
</template>

<script>
import {
    Auth
} from 'aws-amplify';

export default {
    name: 'Login',

    methods: {
        async userSignIn() {
            await Auth.federatedSignIn({
                provider: 'Google'
            });
        }
    }
}
</script>
