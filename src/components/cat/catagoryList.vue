<template>

<div class="mt-3">
    <div class="container container-fluid">
    <div class="row">
        <div class="table-responsive">
            <table class="table table-striped">
                <thead class="thead-dark">
                    <tr>
                        <th> <span class="font-weight-bold text-info">Name </span></th>
                        <th> <span class="font-weight-bold text-info">Discription </span></th>
                        <th><span class="font-weight-bold text-info">Created</span></th>
                        <th><span class="font-weight-bold text-info">Actions </span></th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="catagory in Catagories" :key="catagory.key">
                        <td>{{ catagory.service_name }}</td>
                        <td>{{ catagory.disc }}</td>
                        <td>{{ catagory.timestamp }}</td>
                        <td>
                            <router-link :to="{name: 'cedit', params: { id: catagory.key }}" class="btn btn-submit"><font-awesome-icon icon="list-ul"></font-awesome-icon>
                            </router-link>
                            
                            
                            <button @click.prevent="deleteCatagory(catagory.key)" class="btn btn-danger"><font-awesome-icon icon="trash"></font-awesome-icon></button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
    </div>
</div>
</template>
<script>
import db from "../../db.js";
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";

    export default {
        data() {
            return {
                Catagories: []
            }
        },
        created() {
            db.collection('catagories').onSnapshot((snapshotChange) => {
                this.Catagories = [];
                snapshotChange.forEach((doc) => {
                    this.Catagories.push({
                        key: doc.id,
                        service_name: doc.data().service_name,
                        disc: doc.data().disc,
                        timestamp: doc.data().timestamp,

                    })
                });
            })
        },
        components: {
            FontAwesomeIcon
        },
        methods: {
            deleteCatagory(id){
              if (window.confirm("Do you really want to delete?")) {
                db.collection("catagories").doc(id).delete().then(() => {
                    console.log("Document deleted!");
                })
                .catch((error) => {
                    console.error(error);
                })
              }
            }
        }
    }
</script>

<style>
    .btn-primary {
        margin-right: 12px;
    }
</style>
