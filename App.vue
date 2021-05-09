<template>
  <div id="app">
    <header>
      <h1>My Music</h1>
    </header>
    
    <main>
      <section class= "player">
        <h2 class= "song-title">{{current.title}} - <span>{{current.artist}}
          </span></h2>
          <div class="controls">
          <button class="prev"  @click="prev">Prev</button>
          <button class="play" v-if="!isPlaying" @click="play">Play</button>
          <button class="pause" v-else @click="pause">Pause</button>
          <button class="next" @click="next">Next</button>
        </div>
        </section>
        <section class="playlist">
          <h3>My Playlist</h3>

          <button v-for="song in songs" :key="song.src" @click="play(song)" :class="(song.src
          == current.src) ?'song playing' : 'song'">
          {{song.title}} - {{song.artist}}
          </button>
        </section>
    </main>



  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      current: {},
      index: 0,
      isPlaying: false,
      songs: [
        {
          title: 'Jumping Ships',
          artist: 'Amaarae',
          src: require('./assets/amaarae_jumping_ship.mp3')
        },
        {
          
          title: 'Beg Friend',
          artist: 'Tobi',
          src: require('./assets/beg_friend.mp3')

        },
        {
          title: 'This Sht',
          artist: 'AYLO',
          src: require('./assets/This_sht.mp3')
        }
      ],
      player: new Audio()
    }

  },
  methods: {
    play (song) {
      if (typeof song.src != "undefined") {
        this.current = song;
        this.player.src = this.current.src;
        }
         this.player.play();
         this.player.addEventListener('ended', function (){
        this.index++;
         if (this.index>this.songs.length-1) {
        this.index = 0;
      }
      this.current= this.songs[this.index];
      this.play(this.current);
         }.bind(this))
         this.isPlaying = true;

    },
    pause() {
      this.player.pause();
      
      this.isPlaying = false;
    },


next (){
      this.index ++;
      if (this.index>this.songs.length-1) {
        this.index = 0;
      }
      this.current= this.songs[this.index];
      this.play(this.current);
    },
    prev() {
      this.index--;
      if(this.index<0){
        this.index = this.songs.length -1;

      }
       this.current= this.songs[this.index];
      this.play(this.current);
    }
  },

    
  created () {
    this.current = this.songs[this.index];
    this.player.src = this.current.src
    
  }

}
</script>


<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  body{
    font-family: sans-serif;
    font-display: ;
    background-color: hsla(0, 0%, 0%, 0.897);
  }
  header{
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    background-color: rgba(97, 60, 11, 0.863);
  }
  main{
    width: 100%;
    max-width: 750px;
    margin: 0 auto ;
    padding: 25px;
  }
  .song-title {
    color: rgb(206, 120, 8);
    font-size: 32px;
    font-weight: 700;
    text-transform: uppercase;
    text-align: center;
  }
  .song-title span{
    color: rgb(180, 102, 6);
    font-size: 32px;
    font-style: italic;
    font-weight: 400;
    text-transform: uppercase;
    text-align: center;
    }
  
  .controls {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 30px 15px;
  }
  
  button {
    appearance: none;
    background: none;
    border: none;
    outline: none;
    cursor: pointer;
  }
  .play, .pause {
    font-size: 30px;
    font-weight: 600;
    padding: 15px 25px;
    margin:0px 15px;
    border-radius: 8px;
    color: rgb(63, 27, 2);
    background-color:rgba(97, 60, 11, 0.863) ;
  }
 
  button:hover{
    opacity: 0.8;
  }
  .prev, .next{
    font-size:16px;
    font-weight: 700;
    padding: 10px 20px;
    margin:0px 15px;
    border-radius: 6px;
    color: rgb(63, 27, 2);
    background-color: rgb(197, 136, 92) ;
  }
    .playlist  h3{
    color: rgb(158, 90, 7);
    font-size: 18px;
    font-weight: 700;
    font-style:normal ;
    text-transform: uppercase;
    text-align: center;
  }
  .playlist .song{
    color: rgb(131, 108, 108);
    display: block;
    width:100%;
    padding: 15px;
    font-size:20px;
    font-weight: 700;
    cursor: pointer;
  }
  .playlist.song:hover{
    color: rgb(221, 133, 70);
  }
  .playlist .song.playing{
    color:rgba(161, 84, 29, 0.986);
    background-image:linear-gradient(to right,chocolate,  rgb(209, 170, 142));
  }
  
</style>
