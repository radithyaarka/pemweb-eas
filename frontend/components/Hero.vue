<template>
  <div :style="{ backgroundImage: 'url(https://picsum.photos/id/16/2500/1667/)', height: 'calc(100vh - 64px)' }"
    class="bg-primary text-white py-16 bg-cover bg-center relative">
    <div class="absolute inset-0 bg-black opacity-50"></div>
    <div class="container mx-auto text-center relative z-10">
      <h1 class="text-4xl font-bold mb-4">Welcome to Our Website</h1>
      <p class="text-lg">Please register down below.</p>

      <div class="carousel-container mt-12">
        <transition name="fade" mode="out-in">
          <div :key="currentIndex" class="carousel-item" v-if="blogPosts.length > 0">
            <div class="flex">
              <div class="w-12 pl-5 pr-5" v-if="blogPosts[currentIndex]">
                <div class="bg-white rounded-lg overflow-hidden shadow-lg relative h-full">
                  <img :src="blogPosts[currentIndex].image" alt="Article Image"
                    class="w-full h-48 object-cover object-center">
                  <div class="p-4 h-full mb-11">
                    <h2 class="text-xl font-semibold mb-2 text-gray-600">{{ blogPosts[currentIndex].title }}</h2>
                    <p class="text-gray-600 leading-relaxed">{{ truncatedContent }}</p>
                    <router-link :to="{ name: 'id', params: { id: blogPosts[currentIndex].id } }"
                      class="block absolute bottom-0 left-0 w-full bg-primary text-white text-center font-semibold py-2 hover:bg-accent transition duration-300 ">
                      Read more
                    </router-link>
                  </div>
                </div>
              </div>

              <div class="w-12 pr-5 pl-5">
                <div v-if="nextIndex < blogPosts.length"
                  class="bg-white rounded-lg overflow-hidden shadow-lg relative h-full">
                  <img :src="blogPosts[nextIndex].image" alt="Article Image"
                    class="w-full h-48 object-cover object-center">
                  <div class="p-4 h-full mb-11">
                    <h2 class="text-xl text-gray-600 font-semibold mb-2">{{ blogPosts[nextIndex].title }}</h2>
                    <p class="text-gray-600 leading-relaxed">{{ nextTruncatedContent }}</p>
                    <router-link :to="{ name: 'id', params: { id: blogPosts[nextIndex].id } }"
                      class="block absolute bottom-0 left-0 w-full bg-primary text-white text-center font-semibold py-2 hover:bg-accent transition duration-300 ">
                      Read more
                    </router-link>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </transition>

        <div class="carousel-controls mt-3 flex items-center">
          <button @click="prevSlide" class="carousel-button">
            <span class="text-white">&#8249;</span>
          </button>
          <button @click="nextSlide" class="carousel-button">
            <span class="text-white">&#8250;</span>
          </button>
        </div>
      </div>

      <div class="mt-12">
        <router-link to="/blogdetail"
          class="bg-primary text-white font-semibold py-3 px-6 rounded-full hover:bg-accent">Explore
          More</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogPosts: [],
      currentIndex: 0,
    };
  },
  computed: {
    nextIndex() {
      // Calculate the next index
      return (this.currentIndex + 1) % this.blogPosts.length;
    },
    truncatedContent() {
      return this.getContent(this.currentIndex);
    },
    nextTruncatedContent() {
      return this.getContent(this.nextIndex);
    },
  },
  mounted() {
    // Fetch data from your API
    fetch('http://localhost:3100/api/blog/')
      .then(response => response.json())
      .then(data => {
        // Check if 'docs' property is an array
        if (Array.isArray(data.docs)) {
          // Update the blogPosts data property with the fetched data
          this.blogPosts = data.docs.map(post => ({
            id: post.id,
            title: post.title,
            content: post.content,
            date: post.date,
            writer: post.writer,
            image: post.image,
          }));

          this.startSlideshow();
        } else {
          console.error('API response does not contain an array in the "docs" property:', data);
        }
      })
      .catch(error => {
        console.error('Error fetching data:', error);
      });
  },
  methods: {
    startSlideshow() {
      setInterval(this.nextSlide, 5000); // Change slide every 5 seconds (adjust as needed)
    },
    nextSlide() {
      this.currentIndex = (this.currentIndex + 1) % this.blogPosts.length;
    },
    prevSlide() {
      this.currentIndex = (this.currentIndex - 1 + this.blogPosts.length) % this.blogPosts.length;
    },
    getContent(index) {
      if (this.blogPosts[index]) {
        const content = this.blogPosts[index].content;
        // Use regex to split the content into words and limit to 20 words
        const truncatedWords = content.split(/\s+/).slice(0, 35).join(' ');
        return `${truncatedWords}...`;
      }
      return '';
    },
  },
};
</script>


<style scoped>
.bg-primary {
  background-color: #123C69;
}

.text-primary {
  color: #123C69;
}

.bg-accent {
  background-color: #AC3B61;
}

.text-accent {
  color: #AC3B61;
}

.text-muted {
  color: #BAB2B5;
}

.container {
  padding-left: 1rem;
  padding-right: 1rem;
}

.bg-cover {
  background-size: cover;
}

.bg-center {
  background-position: center center;
}

.absolute {
  position: absolute;
}

.bottom-0 {
  bottom: 0;
}

.left-0 {
  left: 0;
}

.py-2 {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}

.overflow-hidden {
  overflow: hidden;
}

.leading-relaxed {
  line-height: 1.6;
}

.rounded-lg {
  border-radius: 0.5rem;
}

.transition {
  transition-property: background-color, border-color, color, fill, stroke, opacity, box-shadow, transform;
  transition-timing-function: cubic-bezier(0.4, 0, 0.2, 1);
}

.transition:hover {
  transform: translateY(-2px);
}

.rounded-full {
  border-radius: 9999px;
}

.carousel-container {
  position: relative;
}

.carousel-item {
  display: inline-block;
  width: 100%;
}

.w-12 {
  width: 50%;
}

.pr-2 {
  padding-right: 0.5rem;
}

.pl-2 {
  padding-left: 0.5rem;
}

.carousel-item a:hover {
  background-color: #AC3B61 !important;
}

.carousel-controls {
  display: flex;
  justify-content: center;
  align-items: center;
}

.carousel-button {
  background-color: #123C69; /* Accent color */
  border: none;
  color: white;
  font-size: 1rem;
  cursor: pointer;
  padding: 0.2rem 0.8rem;
  margin: 0.5rem;
  border-radius: 0.25rem;
  transition: background-color 0.3s ease-in-out;
}

.carousel-button:hover {
  background-color: #BF5069; /* Darker shade for hover effect */
}
</style>
