<template>
  <div class="container monda-font">
    <nav>
      <img src="@/assets/log2.png" alt="" />
    </nav>
    <div>
      <h2 class="monda-font">Connexion</h2>
      <p class="stext monda-font">Retrouver l’activité de vos véhicules dans un seul <br> endroit</p>
  </div>
    <form @submit.prevent="authenticate">

      <div class="input-field">
        <div><label for="email">Telephone/Email</label></div>
      <input type="email" id="email" v-model="email" placeholder="00 - 000 - 000 - 000" required>
      </div>
      <div class="input-field">
        <div> <label for="password">Mot de passe</label></div>
        <input type="password" id="password" v-model="password" placeholder="Entrez votre mot de passe" required>
      </div>
      <div>
        <a class="mot" href="">Mot de passe oublié ? </a>
      <button class="btn" type="submit">Connexion</button>
      </div>
    </form>
    <p class="pas">Pas de compte? <router-link to="/">Inscription</router-link></p>
  </div>
</template>

<script>
import { initializeApp } from 'firebase/app';
import { getAuth, signInWithEmailAndPassword } from 'firebase/auth';

// Configuration de Firebase
const firebaseConfig = {
  apiKey: "AIzaSyBw2cJyhoP4FKACMKqTfaa1WunX643K_Dc",
  authDomain: "opep-9253f.firebaseapp.com",
  projectId: "opep-9253f",
  storageBucket: "opep-9253f.appspot.com",
  messagingSenderId: "127293039145",
  appId: "1:127293039145:web:2fb2252039b0c3fa143238"
  // ...
};

// Initialisation de l'application Firebase
const firebaseApp = initializeApp(firebaseConfig);
const auth = getAuth(firebaseApp);

export default {
  name: 'AuthentificationPage',
  data() {
    return {
      email: '',
      password: ''
    };
  },
  methods: {
    authenticate() {
      signInWithEmailAndPassword(auth, this.email, this.password)
        .then(userCredential => {
          // Connexion réussie
          console.log(userCredential);
          alert('Connexion avec sucess!!')
          this.$router.push('/ajouterV');
        })
        .catch(error => {
          // Gestion des erreurs
          console.error(error);
        });
    }
  }
};
</script>

<style scoped>
h2{
    font-size: 30px;
    font-weight: bold;
    color: rgba(6, 40, 61, 1);
}
.stext{
    margin-top: -20px;
    color: rgba(0, 0, 0, 0.2);
    font-size: 13px;
}
.container{
    text-align: left;
    margin-left: 10px;
    width: 100%;

}
form{
    width: 100%;
}
.monda-font {
    font-family: 'Monda', sans-serif;
  }
body{
    
}
.input-field{
    margin-top: 30px;    
}
input{
width: 90%;
height: 40px;
margin-top: 7px;
border-color: rgba(0, 0, 0, 0.2);
outline: none;
}
input:nth-child(2){
    margin-bottom: 20px;
}
label{
    font-weight: bold;
    font-size: 20px;
    color: rgba(6, 40, 61, 1);

}
.mot{
    color: rgba(6, 40, 61, 1);
    font-weight: 500;
}
.btn{
    margin-top: 20px;
    font-size: 17px;
    background: rgba(51, 167, 226, 1);
    border: none;
    width: 94%;
    border-radius: 5px;
    height: 45px;
    color: white;
    
}
.pas{
    font-weight: 700;
    color: rgba(6, 40, 61, 1);
}
.pas a{
    text-decoration: none;
    color: rgb(214, 106, 5);
}
</style>