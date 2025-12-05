<script setup lang="ts">
import {SidebarInset, SidebarProvider} from "@/components/ui/sidebar";
import AppSidebar from "@/components/layout/AppSidebar.vue";
import AppHeader from "@/components/layout/AppHeader.vue";
</script>

<template>
  <SidebarProvider>
    <AppSidebar />
    <SidebarInset>
      <AppHeader />
      <main class="min-h-screen bg-base-20 pl-8 pr-10 pt-14 pb-10">
        <router-view />
      </main>
    </SidebarInset>
  </SidebarProvider>
</template>

<style scoped lang="scss">

</style>