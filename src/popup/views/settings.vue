<template>
  <v-row no-gutters class="fill-height settings">
    <v-col cols="4" class="my-1">
      <v-card
        class="mx-1 py-2 fill-height d-flex justify-center align-center settings_addPac"
        elevation="0"
        outlined
        @click="goToAddPage"
      >
        <span class="white--text body-1"><v-icon small color="white">mdi-plus</v-icon> Add New</span>
      </v-card>
    </v-col>
    <v-col cols="4" v-for="(item, id) in pacs" :key="id" class="my-1">
      <v-card
        @click="goToEditPage(item)"
        class="mx-1 py-2 fill-height d-flex justify-center align-center"
        elevation="0"
        outlined
        :color="color(item.name)"
      >
        <span class="body-1" :style="{ color: stringToShade(item.name) }">
          <v-icon small :color="stringToShade(item.name)">mdi-pencil</v-icon> {{ item.name }}
        </span>
      </v-card>
    </v-col>
  </v-row>
</template>

<script lang="ts">
import Vue from 'vue'
import Component from 'vue-class-component'
import { Dictionary } from 'vue-router/types/router'
import stringToColor from 'string-to-color'
import stringToShade from '@/utils/stringToShade'
import { PAGE } from '@/constants'

@Component
export default class Settings extends Vue {
  get pacs() {
    return this.$s.getter.sortedPacs
  }
  goToAddPage() {
    this.$router.push({ name: PAGE.addPac })
  }

  color(name: string) {
    return stringToColor(name)
  }

  stringToShade(name: string) {
    return stringToShade(name)
  }

  goToEditPage(pac: { name: string; url: string }) {
    this.$router.push({ name: PAGE.editPac, params: ({ pac } as unknown) as Dictionary<string> })
  }
}
</script>
<style lang="scss" scoped>
.settings {
  &_addPac {
    background: linear-gradient(90deg, #bf0000, #665cac);
  }
}
</style>
