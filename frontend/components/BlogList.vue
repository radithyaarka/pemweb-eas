<template>
  <div>
    <section class="container mx-auto my-16">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div v-for="post in blogPosts" :key="post.id" class="rounded-lg overflow-hidden shadow-md h-full">
          <div class="bg-primary relative h-full flex flex-col">
            <img :src="post.image" alt="Blog Post Image" class="w-full h-64 object-cover">
            <div class="p-4 flex-grow flex flex-col justify-between">
              <div>
                <h2 class="text-xl font-bold mb-2 text-white">{{ post.title }}</h2>
                <div class="post-content-container flex-grow">
                  <p class="text-white rounded mb-5">{{ truncateContent(post.content) }}</p>
                </div>
              </div>
              <div class="flex flex-col items-start mt-2">
                <router-link v-if="post.content.length > 20" :to="{ name: 'id', params: { id: post.id } }"
                  class="inline-block px-3 py-1 text-white border border-white hover:bg-red-500 transition duration-300 ease-in-out transform hover:scale-105 text-sm rounded-full">Read
                  More</router-link>
                <p class="text-muted">{{ post.writer }} - {{ formatDate(post.date) }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Error Handling -->
    <div v-if="error" class="container mx-auto my-16">
      <div class="text-center">
        <h2 class="text-2xl font-bold text-accent">Oops! Something went wrong.</h2>
        <p class="text-primary">{{ error }}</p>
        <router-link to="/" class="inline-block mt-4 px-3 py-1 text-white bg-primary border border-white hover:bg-red-500 transition duration-300 ease-in-out transform hover:scale-105 text-sm rounded-full">Back to Home</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      blogPosts: [],
      error: null,
    };
  },
  created() {
    // Fetch data from your API
    fetch('http://localhost:3100/api/blog/')
      .then(response => {
        if (!response.ok) {
          throw new Error(`HTTP error! Status: ${response.status}`);
        }
        return response.json();
      })
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
        } else {
          console.error('API response does not contain an array in the "docs" property:', data);
          this.error = 'Invalid data format from the server.';
        }
      })
      .catch(error => {
        console.error('Error fetching data:', error);
        this.error = 'Failed to fetch data from the server.';
      });
  },

  methods: {
    formatDate(date) {
      return new Date(date).toLocaleDateString();
    },
    truncateContent(content) {
      const words = content.split(' ');
      if (words.length > 20) {
        return words.slice(0, 35).join(' ') + '...';
      }
      return content;
    },
  },
};
</script>
  
  <style scoped>
  /* Add scoped styles here if needed */
  
  /* Color Palette */

  .post-content-container {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
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
  
  /* Responsive Padding */
  .container {
    padding-left: 1rem;
    padding-right: 1rem;
  }
  
  .transition {
    transition: all 0.3s ease-in-out;
  }
  
  /* Optional: Add a hover effect to scale the button */
  .hover\:scale-105:hover {
    transform: scale(1.05);
  }
  
  /* Change the background color on hover to red */
  .hover\:bg-red-500:hover {
    background-color: #AC3B61;
    /* Red background color */
  }
  </style>
  