<template>
    <div>
        <!-- TODO: Crear componente GitHub -->
        <div>
            <input type="text" placeholder="escribir" v-model="user" @keydown.enter="obtenerUsuario">
        </div>

        <div v-if="userValid">
            {{ userValid.login }}

            <br>
            <img :src="userValid.avatar_url">
            <a :href="userData.html_url"> URL de repositorio</a>
            <button type="button" @click="obtenerRepositorios"> Repositorios </button>
        </div>
    
        <div v-if="userRepoVald">
            <GitHubRepos :repolist="userRepo"> </GitHubRepos>
        </div>
    
    </div>
    
</template>

<script>

import GitHubRepos from "./GitHubRepos.vue"
// TODO: Importar componente GitHubRepos

export default {
    name: 'GitHub',
    components: {
        GitHubRepos
    },
    data: function() {
        return {
            user: "",
            userData: {},
            userRepo: {},
            userValid: false,
            userRepoVald: false,
        }
    },
    methods: {
        obtenerUsuario: function() {

            var userAuth = process.env.VUE_APP_USERNAME || "user";
            var passAuth = process.env.VUE_APP_USERTOKEN || "pass";

            let headers = new Headers();
            headers.set('Authorization', 'Basic ' + btoa(userAuth + ":" + passAuth));
            
            var url = "https://api.github.com/users/" + this.user;

            fetch(url, {method:'GET',
                    headers: headers,     
                })
                .then(res => res.json())
                .then(response => {
                console.log(response);
                this.userData= response;
                this.userValid = true;
            });
        },
        obtenerRepositorios: function() {
            var userAuth = process.env.VUE_APP_USERNAME || "user";
            var passAuth = process.env.VUE_APP_USERTOKEN || "pass";

            let headers = new Headers();
            headers.set('Authorization', 'Basic ' + btoa(userAuth + ":" + passAuth));
            
            var url = this.userData.repos_url;

            fetch(url, {method:'GET',
                    headers: headers,     
                })
                .then(res => res.json())
                .then(response => {
                console.log(response);
                this.userRepo= response;
                this.userRepoVald = true;
            });

        }
    }
}
</script>

<style scoped>
</style>
