<template>
    <div class="container monda-font animate__animated animate__fadeInLeft">
      <nav>
        <i class="fa fa-user"></i>
      </nav>
      <div>
        <h2 class="monda-font">Ajouter un véhicule</h2>
        <p class="stext monda-font">Veuillez renseigner des informations sur tous les <br>champs ci-dessous</p>
      </div>
      <form @submit.prevent="ajouterVehicule">
        <div class="input-field">
          <div><label for="">Marque véhicule</label></div>
          <input type="text" v-model="marque" placeholder="Ex : Mercedez" required>
        </div>
        <div class="input-field">
          <div><label for="">Modèle</label></div>
          <input type="text" v-model="modele" placeholder="Classe C" required>
        </div>
        <div class="input-field">
          <div><label for="password">Ajouter une image</label></div>
          <input class="selectI" type="file" accept="image/*" @change="selectImage">
          <img class="affiche" :src="selectedImage" v-if="selectedImage">
        </div>
        <div class="button">
          <input class="btn" type="submit" value="Annuler">
          <input class="btn" type="submit" value="Valider">
        </div>
      </form>
    </div>
  </template>
<script>
import { initializeApp } from 'firebase/app';
import { getFirestore, collection, addDoc } from 'firebase/firestore';

// Configuration de Firebase
const firebaseConfig = {
    apiKey: "AIzaSyBw2cJyhoP4FKACMKqTfaa1WunX643K_Dc",
  authDomain: "opep-9253f.firebaseapp.com",
  projectId: "opep-9253f",
  storageBucket: "opep-9253f.appspot.com",
  messagingSenderId: "127293039145",
  appId: "1:127293039145:web:2fb2252039b0c3fa143238"
};

// Initialisation de l'application Firebase
const firebaseApp = initializeApp(firebaseConfig);
const db = getFirestore(firebaseApp);

export default {
  name: 'AddVehicle',
  data() {
    return {
      marque: '',
      modele: '',
      selectedImage: null
    };
  },
  methods: {
    async ajouterVehicule() {
      const vehicle = {
        marque: this.marque,
        modele: this.modele,
        imageUrl: this.selectedImage
      };

      try {
        const docRef = await addDoc(collection(db, 'vehicles'), vehicle);
        console.log('Véhicule ajouté avec ID:', docRef.id);
        alert('Ajouter avec sucess!')
        this.$router.push('/MesVehicules');
      } catch (error) {
        console.error('Erreur lors de l\'ajout du véhicule:', error);
      }
    },
    selectImage(event) {
      // Logique pour sélectionner une image
      const file = event.target.files[0];
      if (file) {
        // Utilisez par exemple FileReader pour lire l'image et la stocker dans selectedImage
        const reader = new FileReader();
        reader.onload = (e) => {
          this.selectedImage = e.target.result;
        };
        reader.readAsDataURL(file);
      }
    }
  }
};
</script>
<style scoped>
.selectI{
    color: white;
    border: 1px solid rgba(0, 0, 0, 0.2);
    
    width: 90%;
}
.tdepense{
    width: 90.5%;
    display: flex;
    justify-content: space-between;
}
.tdepense input{
    width: 26%;
    text-align: center;
}
h2{
    font-size: 30px;
    font-weight: bold;
    color: rgba(6, 40, 61, 1);
    margin-top: 70px!important;
}
.stext{
    margin-top: -20px;
    color: rgba(0, 0, 0, 0.2);
    font-size: 13px;
}
.container{
    text-align: left;
    margin-left: 20px;
    width: 100%;

}
form{
    width: 100%;
}
.monda-font {
    font-family: 'Monda', sans-serif;
  }
  .affiche{
    width: 90%;
    height: 300px;
  }
.input-field{
    margin-top: 30px;    
}
input{
width: 87%;
height: 40px;
margin-top: 7px;
border-color: rgba(0, 0, 0, 0.2);
outline: none;
}
label{
    font-weight: 550;
    font-size: 20px;
    color: rgba(6, 40, 61, 1);

}
.mot{
    color: rgba(6, 40, 61, 1);
    font-weight: 500;
}
.button{
    width: 90.5%;
    justify-content: space-between;
    display: flex;
}
.btn{
    margin-top: 20px;
    font-size: 15px;
    background: rgba(51, 167, 226, 1);
    border: none;
    width: 47%;
    height: 45px;
    color: white;
    
}
.btn:nth-child(1){
    background-color: transparent;
    color: rgba(6, 40, 61, 1);
    border: 1px solid rgba(6, 40, 61, 1);
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