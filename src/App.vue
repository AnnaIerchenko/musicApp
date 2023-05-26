<script setup>
import { onBeforeMount } from 'vue'
import { RouterLink, RouterView } from 'vue-router'
import Magnify from 'vue-material-design-icons/Magnify.vue'
import Bell from 'vue-material-design-icons/Bell.vue'
import SideMenuItem from './components/SideMenuItem.vue'
import MusicPlayer from './components/MusicPlayer.vue'
import SongLyrics from './components/SongLyrics.vue'

import { useSongStore } from './stores/song'
import { storeToRefs } from 'pinia'
const useSong = useSongStore()
const {isPlaying, currentTrack, isLyrics, trackTime} = storeToRefs(useSong)

onBeforeMount(() => {
  isPlaying.value = false
  isLyrics.value = false
  trackTime.value = '0:00'
})
</script>

<template>
  <div
    id="TopNav"
    class="fixed right-0 flex items-center justify-between w-[calc(100%-240px)] h-[56px] border-b border-b-[#32323d]"
  >
    <div class="flex items-center w-full">
      <Magnify class="pl-6 mt-1 pr-2" fillColor="#7e7e88" :size="22" />
      <input 
        class="p-1 bg-transparent outline-none font-[300] placeholder-[#bebec7] text-[#ffffff] w-full max-w-xl"
        placeholder="Search"
        type="text"
      />
    </div>
    <div class="flex items-center pr-10">
      <div class="mr-4 p-1 hover:bg-gray-600 rounded-full cursor-pointer">
        <Bell fillColor="#ffffff" :size="20"/>
      </div>
      <img
        class="rounded-full w-[32px]" 
        src="https://picsum.photos/id/147/300/300"
        alt="pic">
    </div>
  </div>

  <div
    id="SideNav"
    class="fixed w-[240px] bg-[#191922] h-[100vh] border-r border-r-[#323230]"
  >
    <div class="w-full pl-6 pt-3 cursor-pointer ">
      <RouterLink to="/">
       <img width="130" src="/images/deezer-logo.png" alt="">
      </RouterLink>
    </div>

    <div class="mt-[53px]"></div>

    <SideMenuItem 
      iconString="music"
      :iconSize="20"
      pageUrl="/"
      name="Music"
    />
    <SideMenuItem 
      iconString="podcast"
      :iconSize="20"
      pageUrl="/podcasts"
      name="Podcasts"
    />
    <SideMenuItem 
      iconString="explore"
      :iconSize="20"
      pageUrl="/artist"
      name="Explore"
    />
    <SideMenuItem 
      iconString="favourite"
      :iconSize="20"
      pageUrl="/favourite"
      name="Favourites"
    />

    <div class="text-[#a2a2ad] font-light text-[12px] pl-[62px] mt-[25px]">
      <div class="py-[9px] hover:text-[#ef5465] cursor-pointer">Favourite tracks</div>
      <div class="py-[9px] hover:text-[#ef5465] cursor-pointer">Playlist</div>
      <div class="py-[9px] hover:text-[#ef5465] cursor-pointer">Albums</div>
      <div class="py-[9px] hover:text-[#ef5465] cursor-pointer">Artists</div>
      <div class="py-[9px] hover:text-[#ef5465] cursor-pointer">Podcases</div>
    </div>
  </div>

  <!-- central display -->
  <div class="fixed w-[calc(100%-240px)] h-[calc(100%-56px)] ml-[240px] mt-[56px] overflow-x-auto">

    <RouterView />
  </div>

  <MusicPlayer v-if="currentTrack"/>

  <SongLyrics 
    v-if="isLyrics"
    :class="{'animate__animated animate__slideInUp animate__faster' : isLyrics}"
  />
</template>
 
<style scoped>


</style>
