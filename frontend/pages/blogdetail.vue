<template>
    <div>
      <Navbar />
      <header class="blog-header" :style="{ backgroundImage: 'url(https://media.giphy.com/media/Id71NFYfSBOKv2IexE/giphy-downsized-large.gif)' }">
        <div class="header-content">
          <h1>Check your registration status</h1>
          <p>Down below.</p>
        </div>
      </header>
      <div>
        <status />
      </div>
      <Footer />
    </div>
  </template>
  
  <script>
  export default {};
  </script>
  
  <style scoped>
  body,
  html {
    height: 100%;
    margin: 0;
    padding: 0;
    background-color: #f9f9f9;
  }
  
  .blog-header {
    position: relative;
    background-size: cover;
    background-position: center;
    height: 400px; /* Adjust the height based on your design */
    display: flex;
    align-items: center;
  }
  
  .blog-header::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: black;
    opacity: 0.5; /* Adjust the opacity as needed */
  }
  
  .blog-header .header-content {
    position: relative;
    z-index: 1;
    text-align: center;
    color: #fff; /* Adjust text color as needed */
    margin: 0 auto; /* Center horizontally */
    max-width: 600px; /* Adjust max-width based on your design */
  }
  
  .blog-header .header-content h1 {
    font-size: 2.5em;
    margin-bottom: 10px;
  }
  
  .blog-header .header-content p {
    font-size: 1.2em;
    color: #ecf0f1;
    margin: 0;
  }
  </style>
  