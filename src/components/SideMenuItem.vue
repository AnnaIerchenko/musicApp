<script setup>
import {toRefs, ref, watchEffect} from 'vue'
import { RouterLink, useRouter} from 'vue-router'

const route = useRouter()
const props = defineProps({
  iconString: String,
  iconSize: Number,
  pageUrl: String,
  name: String,
})

const { iconString, pageUrl, name} = toRefs(props)
let icon = ref(null)
// active and not active icon
watchEffect(() => {
  if(route.path == pageUrl.value && icon.value === iconString.value + '-red') return
  if(route.path == pageUrl.value){
    icon.value = iconString.value + '-red'
  }else {
    icon.value = iconString.value + '-white'
  }
})

const isHover = () => {
  if(icon.value == iconString.value + '-red'){
    icon.value = iconString.value + '-white'
  }else if (icon.value === iconString.value + '-white'){
    icon.value = iconString.value + '-red'
  }
}
</script>

<template>
  <div class="flex items-center w-full my-[20px]">
    <RouterLink 
      :to="pageUrl"
      :class="pageUrl === route.path ? 'border-l-[#ef5465] text-[#ef5465]' : 'border-l-[#191922] text-[#ffffff]'"
      class="border-l-4 w-full hover:text-[#ef5465]"
      @mouseenter="$event => isHover()"
      @mouseleave="$event => isHover()"
    >
      <div class="flex items-center pl-3 mx-3 cursor-pointer">
        <img :width="iconSize" :src="`/images/icons/${icon}.png`" alt="pic">
        <div class="pl-3.5 font-[600] text-[17px]">
          {{ name }}
        </div>
      </div>
    </RouterLink>
  </div>
</template>