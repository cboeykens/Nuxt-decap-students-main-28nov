
<template>
  <div class="layout2">
    <ClientOnly>
    
    <!-- Loading Drawer component -->
    <div class="absolute top-0 right-0 z-10 pr-5">
      <Drawer/> 
    </div>

    <!-- Main section -->
    <div class="container mx-auto p-4 animate-fade animate-once animate-delay-[500ms]">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mt-6">
        <!-- First column -->
        <div>
          <h1 class="silkscreen-bold text-4xl md:text-4xl lg:text-6xl lg:mb-3 font-bold">{{ data.title }}</h1>
          <h1 v-if="data.subtitle" class="opacity-80 text-xl md:text-2xl lg:text-3xl roboto-mono-regular pb-5">{{ data.subtitle }}</h1>
          
            <!-- New image element added -->
          <img 
            src="public/img/typo_1.jpg" 
            alt="image of typo poster" 
          />


        </div>

        <!-- Second column -->
        <div class="mt-20">
          <p class="roboto-mono-regular text-lg md:text-2xl lg:text-xl pb-5 font-bold">{{ data.description }}</p>
          <ContentRenderer :value="data"/>
          <div class="mt-5" v-if="data.imagegallery && data.imagegallery.showgallery == true">
            <ImageGallery/> 
          </div>
        </div>
      </div>

      <!-- Second row -->
      <div v-if="data.related_page">
        <RelatedPages :relatedPages="data.related_page"/>
      </div>

      <!-- Link and published date -->
      <div class="text-xs leading-3">
        <hr />
        <p class="text-xs opacity-50 hover:opacity-100 pb-2">Last update: {{ formatDate(data.date) }}</p>
        <article v-if="data.tags" class="tags">
          <li v-for="(item, index) in data.tags" :key="index" class="pt-2 text-xs opacity-50 hover:opacity-100">
            <NuxtLink :to="`/tags/${item}`">{{ item }}</NuxtLink> <!-- Load NuxtLink -->
          </li>
        </article>
      </div>
    </div>

    <!-- Loading the ShareButtons component -->
    <ShareButtons/>

    <!-- SEO metadata -->
    <Title>{{ data.title }}</Title>
    <Meta name="description" :content="data.description" />
    <Meta name="tags" :content="data.tags.join(', ')" />
    <Meta name="keywords" :content="data.tags.join(', ')" />
    <Meta property="og:title" :content="data.title" />
    <Meta property="og:description" :content="data.description" />
    <Meta property="og:image" :content="data.thumbnail" />
    <Meta property="og:url" :content="data.url" />
    <Meta property="og:type" content="article" />
  </ClientOnly>
  </div>

</template>

<script setup>
import { ref } from 'vue';
const imageLoaded = ref(false);

defineProps(['data', 'formatDate']);
</script>

<style scoped>
.spinner {
  border: 4px solid rgba(255, 255, 255, 0.3);
  border-top: 4px solid #fff;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>
