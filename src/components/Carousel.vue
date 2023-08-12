<template>
    <h5 class="text-center mt-5">Vue3 Image Carousel Example</h5>
    <div class="carousel text-center mt-3">
      <img :src="currentImage" alt="Image Carousel" class="img-fluid" />
    </div>
    <div class="text-center mt-3">
      <button @click="prevImage" class="btn btn-primary me-2">Previous</button>
      <button @click="nextImage" class="btn btn-primary">Next</button>
    </div>
  </template>
  
  <script setup>
    import { ref, onMounted, onBeforeUnmount, computed } from 'vue';
    import axios from 'axios';

    const images = ref([]);
    let intervalId = null;



    function startCarousel() {
        intervalId = setInterval(() => {
            nextImage()
        }, 1000);
    }

    function stopCarousel() {
        if (intervalId) {
            clearInterval(intervalId);
            intervalId = null;
        }
    }

    async function fetchImages() {
        try {
            const response = await axios.get('https://picsum.photos/v2/list?page=2&limit=10');
            images.value = response.data.map((imageData) => imageData.download_url);
        } catch (error) {
            console.error('An error occurred when fetching images:', error);
        }
        startCarousel();
    }

    const currentImageIndex = ref(0);

    const currentImage = computed(() => images.value[currentImageIndex.value]);

    function prevImage() {
        currentImageIndex.value = (currentImageIndex.value - 1 + images.value.length) % images.value.length;
    }

    function nextImage() {
        currentImageIndex.value = (currentImageIndex.value + 1) % images.value.length;
    }
    onMounted(() => {
        console.log('Carousel onMounted hooks call');
        fetchImages()
    });

    onBeforeUnmount(() => {
        console.log('Carousel onBeforeUnmount hooks call');
        stopCarousel();
    });
    
  </script>
  
  <style scoped>
  img {
        height: 600px;
        width: 1000px;
    }
  </style>
  