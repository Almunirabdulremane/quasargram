<template>
    <q-page class="constrain q-pa-md">
        <div class="row q-col-gutter-lg">
            <div class="col-12 col-sm-8">
                <q-card v-for="post in posts" :key="post.id" class="card-post" flat bordered>
                    <q-item>
                        <q-item-section avatar>
                        <q-avatar>
                            <img src="../../public/image/minhafoto.jpg">
                        </q-avatar>
                        </q-item-section>

                    <q-item-section>
                    <q-item-label class="text-bold">Almunir_Abdulremane</q-item-label>
                    <q-item-label caption>
                            {{ post.location }}
                    </q-item-label>
                    </q-item-section>
                    </q-item>

            <q-separator />
                    <q-img
                    :src="post.imageUrl"
                         basic
                     />
                 <q-card-section>
                    <div class="">{{ post.caption }}</div>
                    <div class="text-caption text-grey">{{ post.date | niceDate }}</div>
                </q-card-section>

            </q-card>
        </div>

        <div class="col-4 large-screen-only">
                    <q-item class="fixed">
                        <q-item-section avatar>
                            <q-avatar sixe="48px">
                                <img src="../../public/image/minhafoto.jpg">
                            </q-avatar>
                        </q-item-section>

                        <q-item-section>
                            <q-item-label class="text-bold">Almunir_Abdulremane</q-item-label>
                            <q-item-label caption>
                                Almunir Abdulremane
                            </q-item-label>
                        </q-item-section>
                    </q-item>
        </div>
        </div>
        
    

    </q-page>
</template>

<script>
import { date } from 'quasar'
export default {
    name: 'PageHome',
    data() {
        return {
            posts: [
                {
                  id: 1,
                  caption: 'Praia de Wimbi',
                  date: '12-01-2023',
                  location: 'Pemba, Mozambique',
                  imageUrl: 'https://cdn.quasar.dev/img/parallax2.jpg'
                },
                {
                  id: 2,
                  caption: 'Ilha de Moçambique',
                  date: '12-01-2023',
                  location: 'Nampula, Mozambique',
                  imageUrl: 'https://cdn.quasar.dev/img/parallax2.jpg'
                },
                {
                  id: 3,
                  caption: 'Montanhas Chimanimani',
                  date: '12-01-2023',
                  location: 'Chimoio, Mozambique',
                  imageUrl: 'https://cdn.quasar.dev/img/parallax2.jpg'
                },
                {
                  id: 4,
                  caption: 'Arquipelago das Quirimbas',
                  date: '12-01-2023',
                  location: 'Cabo delgado, Mozambique',
                  imageUrl: 'https://cdn.quasar.dev/img/parallax2.jpg'
                },
            ]
        }
    },
    filters: {
        niceDate(value) {
            return date.formatDate(value, 'YYYY-MM-DD HH:mm:ss.SSSZ')
        }
    }
}
</script>

<style lang="sass">
    .card-post
        .q-img
            min-height: 200px
</style>