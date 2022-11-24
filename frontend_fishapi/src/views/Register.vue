<template>
    <ion-page>
        <ion-header>
            <ion-row class="ion-align-items-center">
                <ion-col size="3">
                    <a href="/kolam">
                        <font-awesome-icon icon="fa-solid fa-angle-left" style="margin-left: 10%; font-size: 30px;"/>
                    </a>
                </ion-col>
                <ion-col>
                    <h1>Registrasi Kolam</h1>
                </ion-col>
            </ion-row>
        </ion-header>

        <ion-content :fullscreen="true">
            <ion-item class="input">
                <ion-label position="stacked" class="label-input">Nama Kolam</ion-label>
                <ion-input type="text" v-model="nama" name="lokasiName" placeholder="Kolam 1"></ion-input>
            </ion-item>
            <ion-item class="input">
                <ion-label position="stacked" class="label-input">Lokasi Kolam</ion-label>
                <ion-input v-model="lokasi" name="lokasiVar" placeholder="Blok A"></ion-input>
            </ion-item>
            <ion-item class="input">
                <ion-label position="stacked" class="label-input">Jumlah Ikan</ion-label>
                <ion-input type="text" v-model="ikan" name="nomorKolam" placeholder="2A"></ion-input>
            </ion-item>
            <ion-item>
                <ion-label position="stacked" class="label-input-select">Material Kolam</ion-label>
                <ion-select v-model="material" placeholder="Tanah">
                    <ion-select-option value="Tanah">Tanah</ion-select-option>
                    <ion-select-option value="Ubin">Ubin</ion-select-option>
                    <ion-select-option value="Kaca">Kaca</ion-select-option>
                </ion-select>
            </ion-item>
            <ion-item>
                <ion-label position="stacked" class="label-input-select">Bentuk Kolam</ion-label>
                <ion-select v-model="bentuk" placeholder="Bundar">
                    <ion-select-option value="Bundar">Bundar</ion-select-option>
                    <ion-select-option value="Persegi">Persegi</ion-select-option>
                    <ion-select-option value="Segi Tiga">Segi Tiga</ion-select-option>
                </ion-select>
            </ion-item>

            <div class="ion-text-center btn-container">
                <ion-button @click.prevent="addToAPI()">Registrasi</ion-button>
            </div>
        </ion-content>
    </ion-page>
</template>

<script lang="ts">
import {

    IonContent,
    IonPage,
    IonCol,
    IonRow,
    IonSelect,
    IonSelectOption,
    IonInput,
} from "@ionic/vue";
import { defineComponent, onMounted } from "vue";
import axios from 'axios';


export default defineComponent({
    name: "RegisterPage",
    components: {
        IonContent,
        IonPage,
        IonCol,
        IonRow,
        IonSelect,
        IonSelectOption,
        IonInput,
    },
    data() {
        return {
            nama: '',
            lokasi: '',
            ikan:'',
            material: '',
            bentuk: '',
            // pondReg: `kolam : ${nama} location : ${lokasi} material : ${material} bentuk: ${bentuk}` 
        };
    },
    methods: {
        save() {
            var kolam = { "nama": this.nama, "lokasi": this.lokasi, "nomor" : this.ikan, "material": this.material, "bentuk": this.bentuk }
            console.log(kolam)

            onMounted(async () => {
                axios.post('localhost:5000/API/ponds')
                .then(function (response) {
                        console.log(response);
                    })
                .catch(function (error) {
                        console.log(error);
                    });
            })
        },
        addToAPI() {
            let pond = {
                nama: this.nama,
                lokasi: this.lokasi,
                jumlah_ikan: this.ikan,
                material: this.material,
                bentuk: this.bentuk,
            };
            console.log(pond);
            // console.log(this.input_nama)
            // console.log(this.input_lokasi)
            // console.log(this.pilihan1)
            // console.log(this.pilihan2)
            axios.post('http://localhost:5000/API/ponds', pond)
                .then((response) => {
                    this.nama = response.data.nama;
                    this.lokasi = response.data.lokasi;
                    this.ikan = response.data.jumlah_ikan;
                    this.material = response.data.material;
                    this.bentuk = response.data.bentuk;
                })
                .catch((error) => {
                    alert(error);
                })
        }

    },
});
</script>

<style scoped>
#container {
    text-align: center;

    position: absolute;
    left: 0;
    right: 0;
    top: 50%;
    transform: translateY(-50%);
}

#container strong {
    font-size: 20px;
    line-height: 26px;
}

#container p {
    font-size: 16px;
    line-height: 22px;

    color: #8c8c8c;

    margin: 0;
}

#container a {
    text-decoration: none;
}

a:visited {
    color: white;
}

ion-button {
    --background: #1B7C1A;
}

ion-card,
ion-card-title,
ion-card-subtitle {
    color: black;
}

ion-card-title {
    font-weight: bold;
    font-size: 18px !important;
}

ion-card {
    border-radius: 16px;
    margin-bottom: 20px !important;
}

.deactive {
    --background: #952229;
}

.fixedButton {
    /* --border-radius : 50%; */
    position: fixed;
    bottom: 0px;
    right: 0px;
    width: 100px;
    height: auto;
}

ion-item{
    margin-top: 10px !important;
}
.input{
    margin: 0 20px;
}

ion-input{
    --background : #2F2C40;
    border-radius: 10px;
    padding-left: 20px;
    text-indent: 20px;
}

ion-select{
    background-color: #2F2C40;
    border-radius: 10px;
    padding-left: 20px;
    margin: auto;
    width: 90%;
    vertical-align: middle;
}

.label-input{
    font-size: 20px;
    margin-bottom: 15px;
    /* text-align: center; */
}

.label-input-select{
    margin-left: 22px;
    font-size: 20px;
    margin-bottom: 15px;
}

.btn-container{
    margin-top: 40px;
    margin-right: 40px;
    margin-left: 38px;
}

ion-button{
    width: 100%;
    --border-radius: 12px;
    --background:#6C5ECF;
}
</style>

function lokasi(lokasi: any) {
  throw new Error("Function not implemented.");
}
