<template>
  <div class="container">
      <div v-if="photos.length" class="row mb-5">
        <div class="col-sm-12 col-lg-6" v-for="photo in photos" :key="photo._id.$oid">
            <div class="card mb-3 mx-auto">
                <img :src="`http://0.0.0.0:5000/api/file/${photo.name}`" :alt="photo.name" class="p-2 w-100 h-auto">
                <div class="card-body d-flex">
                    <div class="w-50">
                        <b-button pill variant="success" @click="upvote(photo._id.$oid)" class="btn btn-primary w-25 mr-3">+1</b-button>
                        <b-button pill variant="success" @click="downvote(photo._id.$oid)" class="btn btn-danger w-25">-1</b-button>
                    </div>
                    <div class="w-50 text-right">
                        <span v-if="photo.score > 0" class="ml-auto my-auto">Score: +{{ photo.score }}</span>
                        <span v-else class="ml-auto my-auto">Score: {{ photo.score }}</span>
                    </div>
                </div>
            </div>
        </div>
      </div>
      <div v-else class="text-center mt-5">
          <h3>No Photos to display</h3>
      </div>
    <div class="container">
        <div class="row">
            <div class="col-12">
                <div class="mb-5">
                    <h4>Add a photo!</h4>
                    <b-form-file
                        accept="image/jpeg, image/png, image/gif"
                        class="mb-5"
                        @change="fileChange"
                        type="file"
                        v-model="file"
                    >
                    </b-form-file>
                    <b-button pill variant="primary" v-on:click="fileUpload">Upload File</b-button>
                </div>
            </div>
        </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import axios from 'axios'
const apiUrl = "http://0.0.0.0:5000"

@Component({
  components: {
    
  },
})
export default class Home extends Vue {
    photos: Array<{"name": string; "score": number; "_id": {"$oid": string}}> = []
    // eslint-disable-next-line
    file: any = null
    mounted(){
        axios.get(`${apiUrl}/api/photo/allphotos`)
        .then((res) => {
            this.photos = res.data
        })
        .catch((error) => {
            console.error(error)
        });
    }
    upvote(id: string){
        axios.post(`${apiUrl}/api/upvote/${id}`)
        .then((res) => {
            const index = this.photos.findIndex(p => p._id.$oid === id)
            this.photos[index].score = res.data.score
        })
        .catch((error) => {
            console.error(error)
        });
    }
    downvote(id: string){
        axios.post(`${apiUrl}/api/downvote/${id}`)
        .then((res) => {
            const index = this.photos.findIndex(p => p._id.$oid === id)
            this.photos[index].score = res.data.score
        })
        .catch((error) => {
            console.error(error)
        });
    }
    // eslint-disable-next-line
    fileChange(e: any) {
        this.file = e.target.files[0];
    } 
    fileUpload() {
        const payload = new FormData()
        payload.append('new_file', this.file);
        axios.post(`${apiUrl}/api/upload`, payload)
        .then((res) => {
            this.photos.push(res.data)
            this.file = null
        })
        .catch((error) => {
            console.error(error)
        });
    }
}
</script>

<style scoped>


</style>
