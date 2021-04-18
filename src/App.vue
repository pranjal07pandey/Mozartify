<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <h1>Mozartify</h1>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-main>
      <div class="container my-7">
        <section class="player my-5">
          <h2 class="song-title">
            {{ current.title }}
          </h2>
          <span>- {{ current.artist }}</span>

          <div class="text-center my-3">
            <v-btn class="mx-2" fab dark x-large color="indigo" @click="previous" v-if="index!=0">
              <v-icon dark>
                mdi-skip-previous
              </v-icon>
              <small class="mr-1">prev</small>
            </v-btn>

            <v-btn class="mx-2" fab dark x-large  color="indigo" v-else>
              <v-icon dark>
                mdi-skip-previous
              </v-icon>
              <small class="mr-1">prev</small>
            </v-btn>
            <v-btn
              class="mx-2"
              fab
              dark
              x-large
              color="indigo"
              @click="play"
              v-if="!isPlaying"
            >
              <v-icon dark>
                mdi-play
              </v-icon>
              <small class="mr-1">play</small>
            </v-btn>
          
            <v-btn class="mx-2" fab dark x-large color="indigo" @click="pause" v-else>
              <v-icon dark>
                mdi-pause
              </v-icon>
              <small class="mr-1">pause</small>
            </v-btn>

            <v-btn class="mx-2" fab dark x-large  color="indigo" @click="next" v-if="showNext">
              <v-icon dark>
                mdi-skip-next
              </v-icon>
              <small class="mr-1">next</small>
            </v-btn>

            <v-btn class="mx-2" fab dark x-large  color="indigo" v-else>
              <v-icon dark>
                mdi-skip-next
              </v-icon>
              <small class="mr-1">next</small>
            </v-btn>

            <!-- <v-btn class="mx-2" fab dark x-large  color="indigo">
              <v-icon dark>
                mdi-skip-next
              </v-icon>
              <small class="mr-1">next</small>
            </v-btn> -->

            
          </div>

          
        </section>
      </div>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  components: {},

  data: () => ({
    current: "",
    index: 0,
    isPlaying: false,

    totalSongs:0,
    showNext: true,

    songs: [
      {
        title: "Mr. Tambourine Man",
        artist: "Bob Dylan",
        src: require("./assets/mrTambourineMan.flac"),
      },

      {
        title: "Like a Rolling Stone",
        artist: "Bob Dylan",
        src: require("./assets/likeARollingStone.flac"),
      },

      {
        title: "Just Like a Women",
        artist: "Bob Dylan",
        src: require("./assets/justLikeAWomen.flac"),
      },
    ],

    player: new Audio(),
  }),

  mounted() {
    this.controls();
    this.totalSongs = this.songs.length;

    console.log(this.totalSongs)
    // this.player.play();
  },

  methods: {
    controls() {
      this.current = this.songs[this.index];
      this.player.src = this.current.src;
    },

    play() {
      this.player.play();
      this.isPlaying = true;
    },

    pause() {
      this.player.pause();
      this.isPlaying = false;
    },

    next() {
      
      this.index += 1;

      if(this.index < this.totalSongs-1){
        this.showNext = true
        this.controls();

      }

      else{
        this.showNext = false
        this.controls();

      }
      

      this.play();
    },

    previous() {
      this.index -= 1;
      this.controls();
      this.play();
    },
  },
};
</script>
