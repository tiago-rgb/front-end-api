<template>
  <v-bottom-navigation :value="value" color="primary">
      <v-container>
        <div class="d-flex" v-for="(item,id) in info" :key="id" style="margin-top: 100px; margin-left: 200px">
          <img :src="item.image">
          <br>
          {{item.name}}
          <br>
          {{item.status}}
          <br>
          {{item.species}}
          <br>
          {{item.gender}}
        </div>
      </v-container>

        <v-row style="padding-top:80px; padding-right:20px;">
          <v-col v-for="(item,id) in info" :key="id" class="d-flex child-flex" cols="4">
            <v-img :src="item.image" aspect-ratio="1" class="grey lighten-2">
              <template v-slot:placeholder>
                <v-row class="fill-height ma-0" align="center" justify="center">
                  <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                </v-row>
              </template>
            </v-img>
          </v-col>
        </v-row>

  </v-bottom-navigation>
</template>

<script>
import axios from "axios";
export default{
    props : ['id'],
    data () {
    return {
      info: null
        }
    },
    mounted () {
        axios
        .get('https://rickandmortyapi.com/api/character/1,2,3,4,5,6,7,8,9,183')
        .then(response => (this.info = response.data))
        console.log(this.info);
    }
}
</script>