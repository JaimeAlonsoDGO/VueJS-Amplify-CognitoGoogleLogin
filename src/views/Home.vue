<template>
<div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h1>Bienvenido</h1>
    <button @click="userSignOut">Cerrar Sesion</button>
</div>
</template>

<script>
import {
    Auth
} from 'aws-amplify';

export default {
    name: 'Home',
    methods: {
        async userSignOut() {
            try {
                await Auth.signOut();
            } catch (error) {
                console.log('ERROR MIENTRAS CERRABAS SESION: ', error);
            }
        }
    }

}
</script>
