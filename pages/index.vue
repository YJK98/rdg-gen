<template>
  <v-layout column justify-center align-center>
    <v-flex style="width: 97%;" xs12 sm12 md12>
      <div class="text-xs-center">

      </div>
      <v-card>
        <v-card-title class="headline">🥱 of ✍ 📅 for 📃?</v-card-title>
        <v-card-text>

          <v-textarea ref="clone" focused v-model="readings" style="font-size: 20px;" filled auto-grow label="🔮 happens here" rows="8" row-height="30" shaped></v-textarea>
          
          <!-- <div class="text-xs-right">
            💌
          </div> -->
          
        </v-card-text>
        <v-card-actions>
          <v-slider min="0" max="10" v-model="reso" label="Resolution" thumb-color="turquoise" thumb-label="always"></v-slider>
          <v-spacer></v-spacer>
          <!-- <v-btn color="primary" flat nuxt to="/inspire">Continue</v-btn> -->
              
          <v-btn color="primary" large @click="generate">💄</v-btn>
          <v-btn color="primary" large @click="spacing">📑</v-btn>
          <v-btn color="primary" large @click="clip">📄</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
    <v-snackbar v-model="snackbar">Copied</v-snackbar>
  </v-layout>
</template>

<script>
import random from 'random'

export default {
  components: {
  },
  data() {
    return {
      readings: '',
      reso: 0,
      snackbar: false,
      tab: true,
    }
  },
  methods: {
    generate() {
      let ft = ''
      this.readings.split('\n').map(l => {
        let r = l.split(' ').map(Number)
        ft += `${l} ${random.float(...r).toFixed(this.reso)} ${random.float(...r).toFixed(this.reso)} ${random.float(...r).toFixed(this.reso)}\n`
      })
      this.readings = ft
    },
    spacing() {
       
        this.readings = this.tab ? this.readings.replace(/\n/, 'n').replace(/\s/g, '	').replace('n', '\n') : this.readings.replace(/\n/, 'n').replace(/\t/g, ' ').replace('n', '\n')
        this.readings = this.readings.trim()
        this.tab = !this.tab

    },
    clip() {
      this.$refs.clone.focus()
      this.$copyText(this.readings)
      this.snackbar = true
    }
  }
}
</script>
