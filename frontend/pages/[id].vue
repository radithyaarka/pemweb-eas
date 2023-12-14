<template>
  <div class="flex flex-col min-h-screen">
  <div class="single-blog container mx-auto mt-5">
    <div v-if="blogDetails" class="blog-info flex flex-col lg:flex-row items-center lg:items-start gap-8 mt-8">
      <div class="blog-img w-full lg:w-1/2">
        <img :src="blogDetails.image" :alt="blogDetails.title" class="max-h-96 w-full object-cover rounded shadow-md" />
      </div>

      <div class="blog-content w-full lg:w-1/2">
        <h1 class="text-3xl font-bold mb-4 text-primary">{{ blogDetails.title }}</h1>

        <div class="text-lg mb-4">
          <p class="mb-2 text-primary">
            <span class="font-semibold">Date:</span> {{ formatDate(blogDetails.date) }}
          </p>
          <p class="mb-2 text-primary">
            <span class="font-semibold">Writer:</span> {{ blogDetails.writer }}
          </p>
          <p class="text-primary">
            <span class="font-semibold">Content:</span> {{ blogDetails.fullcontent }}
          </p>
        </div>

        <!-- Add any additional content or styling here -->
      </div>
    </div>
    <div class="flex justify-center mt-8 mb-8">
      <nuxt-link
        class="button bg-primary hover:bg-red-500 text-white font-bold py-2 px-4 rounded transition duration-300 ease-in-out transform hover:scale-105"
        to="/"
      >
        Back to Home
      </nuxt-link>

      <nuxt-link
        class="button bg-primary hover:bg-red-500 text-white font-bold py-2 px-4 rounded transition duration-300 ease-in-out transform hover:scale-105 ml-4"
        to="/blogdetail"
      >
        Back to Blog List
      </nuxt-link>
    </div>
  </div>
  <Footer />
</div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      blogDetails: null,
    };
  },
  mounted() {
    this.fetchBlogDetails();
  },
  methods: {
    async fetchBlogDetails() {
      try {
        const blogId = this.$route.params.id;
        const response = await axios.get(`http://localhost:3100/api/blog/${blogId}`);
        const blogData = response.data;

        this.blogDetails = {
          title: blogData.title,
          date: blogData.date,
          writer: blogData.writer,
          fullcontent: blogData.fullcontent,
          image: blogData.image,
        };
      } catch (error) {
        console.error("Error fetching blog details:", error);
      }
    },
    formatDate(date) {
      // Implement your preferred date formatting logic
      return new Date(date).toLocaleDateString();
    },
  },
};
</script>

<style scoped>
/* Add scoped styles here if needed */

/* Color Palette */

.single-blog {
  flex-grow: 1;
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
