<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-grey-10" bordered>
      <q-toolbar class="constrain">

        <q-btn to="/camera" class="large-screen-only q-mr-sm" flat round dense color="dark" icon="eva-camera-outline" size="18px">
        </q-btn>

        <q-separator spaced vertical class="large-screen-only">
        </q-separator>

        <q-toolbar-title class="text-grand-hotel text-bold">
          Quasargram
        </q-toolbar-title>

        <q-btn to="/" class="large-screen-only" flat round dense color="dark" icon="eva-home-outline" size="18px">
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-footer class="bg-white" bordered> 
        <q-tabs v-model="tab" class="text-grey-10" active-color="primary" indicators-color="transparent">

          <q-route-tab to="/" icon="eva-home-outline" label="Home">
          </q-route-tab>
          <q-route-tab to="/camera" icon="eva-camera" label="Camera">
          </q-route-tab>

        </q-tabs>

    </q-footer>

    <q-page-container class="bg-grey-1">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>



export default {
  name: 'MainLayout',
  
  data () {
    return {
      leftDrawerOpen: false,
      essentialLinks: linksData
    }
  }
}
</script>

<style lang="sass">
  .q-toolbar
    @media (min-width: $breakpoint-sm-min)
      height: 77px
  .q-toolbar__title
    font-size: 30px
    @media (max-width: $breakpoint-xs-max)
     text-align: center
  .q-footer
    .q-tab_icon
    font-size: 30px
</style>
