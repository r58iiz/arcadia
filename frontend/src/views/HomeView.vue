<template>
  <div class="announcements">
    <AnnouncementComponent v-for="announcement in recentAnnouncements" :key="announcement.id" :announcement class="announcement" />
  </div>
</template>

<script setup lang="ts">
import { getHome, type ForumPostAndThreadName } from '@/services/api/homeService'
import { onMounted } from 'vue'
import { ref } from 'vue'
import AnnouncementComponent from '@/components/forum/AnnouncementComponent.vue'

const recentAnnouncements = ref<ForumPostAndThreadName[]>()

const fetchHome = async () => {
  getHome().then((data) => {
    recentAnnouncements.value = data.recent_announcements
  })
}

onMounted(() => {
  fetchHome()
})
</script>

<style>
.announcement {
  margin-bottom: 10px;
}
</style>
