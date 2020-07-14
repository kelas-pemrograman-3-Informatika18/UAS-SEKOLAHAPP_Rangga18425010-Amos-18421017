<template>
  <q-layout view="lHh Lpr lFf">
    <q-header unelevated>
      <q-toolbar class="bg-indigo-9">
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          Aplikasi Pendaftaran Siswa
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-deep-purple-5"
    >
      <q-list>
        <q-item-label
          header
          class="text-grey-1"
        >
          Menu Input
        </q-item-label>
        <q-item clickable active-class="active" exact v-ripple :to="{ name:'dashboard'}">
         <q-item-section avatar>
           <q-icon name="dashboard" />
         </q-item-section>

         <q-item-section>
           Dashboard
          </q-item-section>
        </q-item>
        <q-item clickable active-class="active" exact v-ripple :to="{ name:'inputSiswa'}">
         <q-item-section avatar>
           <q-icon name="input" />
         </q-item-section>

         <q-item-section>
           Input Siswa
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container class="bg-blue-grey-2">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false
    }
  }
}
</script>
