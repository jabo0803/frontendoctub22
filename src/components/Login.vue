<template>
    <div class="logIn_user">
        <div class="container_logIn_user">

            <h2>Iniciar sesión</h2>
        <form v-on:submit.prevent="processLogInUser" >
                <input type="text" v-model="user.username" placeholder="Username">
                <br>
                <input type="password" v-model="user.password" placeholder="Password">
                <br>
                <button type="submit">Iniciar Sesion</button>
            </form>
        </div>

    </div>

</template>
<script>
import axios from 'axios';
export default {
name: "LogIn",
    data: function(){
        return {
            user: {
                username:"",
                    password:""
                }
            }
        },
        methods: {
            processLogInUser: function(){
                axios.post(
                "https://mision-tic-bank-be.herokuapp.com/login/",
                this.user,
                {headers: {}}
                )
        .then((result) => {
            let dataLogIn = {
            username: this.user.username,
            token_access: result.data.access,
            token_refresh: result.data.refresh,
            }

            this.$emit('completedLogIn', dataLogIn)

    })
            .catch((error) => {
                if (error.response.status == "401")
            alert("ERROR 401: Credenciales Incorrectas.");

            });
        }
    }
    }
</script>

<style>
.logIn_user{

    margin: 0;
    padding: 0%;
    height: 100%;
    width: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    }
    .container_logIn_user {
    border: 3px solid #283747;
    border-radius: 10px;
    width: 25%;
    height: 60%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    }
    .logIn_user h2{
    color: #283747;
    }
