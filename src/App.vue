<template>
<div id="app">
    <div id="nav">

    </div>
    <router-view />
</div>
</template>

<script>
import {
    Auth,
    Hub
} from 'aws-amplify';

export default {
    methods: {
        async checkUser() {
            Auth.currentAuthenticatedUser()
                .then((user) => {
                    window.console.log(`user: ${JSON.stringify(user)}`);
                })
                .catch(() => {
                    window.console.log('user not logged in');
                });
        },
    },
    async created() {
        // checks user status on load
        await this.checkUser();
    },
    beforeCreate() {
        // listens for all auth events
        Hub.listen('auth', (data) => {
            if (data.payload.event === 'signIn') { // auth signin event
                this.$router.push('/home');
            } else if (data.payload.event === 'signOut') { // auth signout event
                this.$router.push('/');
            }
        });
    }
}
</script>
