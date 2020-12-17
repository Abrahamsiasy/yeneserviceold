<template>
<div class="mt-3">
    <div class="container">
        <div class="row justify-content-center">
        <div class="col-md-5">
            <h3 class="text-center font-weight-bold text-info">Add Catagory</h3>
            <form @submit.prevent="onFormSubmit">
                <div class="form-group">
                    <label>Catagory Name</label>
                    <input type="text" class="form-control" v-model="catagory.name" required>
                </div>

                <div class="form-group">
                    <label>Catagory Discription</label>
                    <textarea rows="5" type="text" class="form-control" v-model="catagory.disc" required>
                    </textarea>
                </div>
                <div>
                    <div
                    class="imagePreviewWrapper"
                    :style="{ 'background-image': `url(${previewImage})` }"
                    @click="selectImage">
                    </div>

                    <input
                    ref="fileInput"
                    type="file"
                    @input="pickFile"
                    @change="uploadeImage">
                </div>
                <div class="form-group">
                    <button class="btn btn-primary btn-block">IPdate catagory</button>
                </div>

            </form>
            <form>
            </form>
            <!-- <Test></Test> -->
        </div>
    </div>
    </div>
</div>
</template>

<script>
import db from "../../db.js";


 import firebase from "firebase";
// import vue2Dropzone from "vue2-dropzone";
// import "vue2-dropzone/dist/vue2Dropzone.min.css";
// import Test from "@/components/cat/test.vue";


    export default {
        // components: {
        //     Test
        // },
        data() {
            return {
                catagory: {
                    name: null,
                    disc: null,
                    image: null
                },
                previewImage: null
            };
        },

        methods: {
            selectImage () {
                    this.$refs.fileInput.click()
                },
                pickFile () {
                    let input = this.$refs.fileInput
                    let file = input.files
                    if (file && file[0]) {
                    let reader = new FileReader
                    reader.onload = e => {
                        this.previewImage = e.target.result
                    }
                    reader.readAsDataURL(file[0])
                    this.$emit('input', file[0])
                    }
            },
            uploadeImage(e){
              console.log(e.target.files[0]);

              let file = e.target.files[0];

              var storageRef = firebase.storage().ref('catagoryIMG/' + file.name);
              let uploadTask = storageRef.put(file);



              uploadTask.on('state_changed', () => {
                // Handle successful uploads on complete
                // For instance, get the download URL: https://firebasestorage.googleapis.com/...
                uploadTask.snapshot.ref.getDownloadURL().then((downloadURL) => {
                  this.catagory.image = downloadURL
                  console.log('File available at', downloadURL);
                });
              });
            },
            onFormSubmit(event) {  
                event.preventDefault()
                db.collection('catagories').add(this.catagory).then(() => {
                    alert("Catagory successfully created!");
                    // const timestamp = Math.round(+new Date()/1000); unix time stamp
                    // var today = new Date();
                    // var date = today.getFullYear()+'/'+(today.getMonth()+1)+'/'+today.getDate();
                    // var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
                    // var timestamp = date+' '+time;
                    this.catagory.name = ''
                    this.catagory.disc = ''
                    this.catagory.image = 'downloadURL'
                    // this.catagory.disc = Test.methods.imageRef.getDownloadURL();
                    this.catagory.timestamp = Math.round(+new Date()/1000)
                
                }).catch((error) => {
                    console.log(error);
                });
            }
        }
    }
</script>


<style scoped lang="scss">
.image-div {
  display: flex;
  margin: 25px;
}
.image {
  max-width: 250px;
  margin: 15px;
}

.imagePreviewWrapper {
    width: 150;
    height: 150px;
    display: block;
    cursor: pointer;
    margin: 0 auto 30px;
    background-size: cover;
    background-position: center center;
}
</style>