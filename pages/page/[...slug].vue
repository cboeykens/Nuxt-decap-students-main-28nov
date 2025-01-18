<template>
  
  <!-- homepage LINK -->
  <div class="flex-1 basis-5/12 pr-1 m-2">
            <NuxtLink to="/">
                    <svg xmlns="http://www.w3.org/2000/svg" width="2em" height="2em" viewBox="0 0 24 24">
                            <path fill="currentColor" d="M5.692 19V9.946L2.604 12.25L2 11.458L12 4l4.346 3.223V5h1.885v3.639l3.788 2.819l-.603.792l-3.089-2.304V19h-5.096v-5.23h-2.462V19zm1-1H9.77v-5.23h4.462V18h3.096V9.21L12 5.256L6.692 9.21zm3.5-7.994h3.616q0-.704-.542-1.159q-.543-.455-1.266-.455t-1.265.453t-.543 1.16M9.77 18v-5.23h4.462V18v-5.23H9.769z"></path>
                    </svg>
            </NuxtLink> 
  </div>

  <div class="mb-20 animate-fade animate-once animate-delay-[500ms]">
    <ContentQuery :path="$route.path" find="one" v-slot="{ data }">
      <component
        :is="getLayoutComponent( data.layoutpage )"
        :data="data"
        :formatDate="formatDate"
      />
    </ContentQuery>
  </div>
</template>

<script setup>
import Layout1 from '~/components/layouts/Layout1.vue';
import Layout2 from '~/components/layouts/Layout2.vue';
import Layout3 from '~/components/layouts/Layout3.vue';
import Layout4 from '~/components/layouts/Layout4.vue';
import Layout5 from '~/components/layouts/Layout5.vue';

// Function to get the corresponding layout component
function getLayoutComponent(layout) {
  switch (layout) {
    case 'layout1':
      return Layout1;
    case 'layout2':
      return Layout2;
    case 'layout3':
      return Layout3;
    case 'layout4':
      return Layout4;
    case 'layout5':
      return Layout5;    
    default:
      return null;
  }
}

// Function to format the date
function formatDate(date) {
  const options = { year: 'numeric', month: 'long' };
  return new Date(date).toLocaleDateString(undefined, options);
}
</script>
