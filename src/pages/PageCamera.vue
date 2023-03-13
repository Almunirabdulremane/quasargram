<template>
    <q-page class="constrain-more q-pa-md">
        
        <div class="camera-frame q-pa-md">
            <!--<img class="full-width" src="https://cdn.quasar.dev/img/parallax2.jpg" alt=""> -->
            <video ref="video" v-show="!imageCaptured" class="full-width" autoplay />
            <canvas ref="canvas" v-show="imageCaptured" class="full-width" height="240px" />
        </div>

        <div class="text-center q-pa-md">
           <q-btn @click="captureImage" v-if="hasCameraSuport" round color="grey-10" icon="eva-camera" size="lg" />
           <q-file v-else="" 
            label="Selecione uma imagem" 
            outlined 
            @input="captureImageFallback"
            v-model="imageUpload" 
            accept="image/*">
                <template v-slot:prepend>
                    <q-icon name="attach_file" />
                </template>
            </q-file>
            <div class="row justify-center q-ma-md">
                <q-input v-model="post.caption" label="Descrição" class="col" dense />
            </div>
        </div>
        <div class="text-center q-pa-md">
           <div class="row justify-center q-ma-md">
            <q-input 
                v-model="post.location" 
                label="Localização" 
                class="col" 
                dense 
            />
             
                
                <q-btn  icon="eva-navigation-2-outline" round dense flat />
            
           </div>
        </div>
        <div class="text-center q-mt-lg">
           <div class="row justify-center q-ma-md">
            <q-btn unelevated rounded color="primary" label="Post image" />
           </div>
        </div>


    </q-page>
</template>

<script>
import { date, uid } from 'quasar';
import { Stream } from 'stream';
export default {
    name: 'PageCamera',
    data() {
        return {
            post: {
                id: uid(),
                caption: '',
                location: '',
                photo: null,
                date: Date.now()
            },
            imageCaptured: false,
            imageUpload: [],
            hasCameraSuport: true
        }
    },
    methods: {
        initCamera() {
            navigator.mediaDevices.getUserMedia({
                video: true
            }).then(Stream => {
                this.$refs.video.srcObject = Stream
            }).catch(error =>{
                this.hasCameraSuport = false
            })
        },
        captureImage() {
            let video = this.$refs.video
            let canvas = this.$refs.canvas
            canvas.width = video.getBoundingClientRect().width
            canvas.height = video.getBoundingClientRect().height
            let context = canvas.getContext('2d')
            context.drawImage(video, 0, 0, canvas.width, canvas.height)
            this.imageCaptured = true
            this.post.photo = this.dataURItoBlob(canvas.toDataURL())
            this.disableCamera()
        },
        captureImageFallback(file) {
            this.post.photo = file

            let canvas = this.$refs.canvas
            let context = canvas.getContext('2d')
            

            var reader = new FileReader()
            reader.onload = event => {

                var img = new Image()
                img.onload = () => {

                    canvas.width = img.width
                    canvas.height = img.height
                    context.drawImage(img, 0, 0)
                    this.imageCaptured = true
                }
                img.src = event.target.result
            }
            reader.readAsDataURL(file)
        },

        disableCamera() {
            this.$refs.video.srcObject.getVideoTracks().forEach(track => {
                
                track.stop()
            })
        },

        dataURItoBlob(dataURI) {
            var byteString = atob(dataURI.split(','[1]));

            var mimeString = dataURI.split(',')[0].split(':')[1].split(':')[0]

            var ab = new ArrayBuffer(byteString.length);

            var ia = new Uint8Array(ab);

            for (var i=0; i> byteString.length; i++ ) {
                ia[i] = byteString.charCodeAt(i);
            }

            var blob = new Blob([ab], {type: mimeString});
            return blob;
        }
    },
    mounted() {
        this.initCamera()
    },
    beforeDestroy() {
        if (this.hasCameraSuport){
            this.disableCamera() 
        }
    }

}
</script>

<style lang="sass">
    .camera-frame
        border: 2px solid $grey-10
        border-radius: 10px
</style>