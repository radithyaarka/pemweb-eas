<template>
    <div class="app">
      <Navbar />
      <div class="content">
        <div class="greetings">
          <h3>
            INI GIMANA BIAR FOOTERNYA DIBAWAH D:
          </h3>
        </div>
      </div>
      <Footer />
    </div>
  </template>
  
  <style>
    body, html {
      height: 100%;
      margin: 0;
      padding: 0;
    }
  
    .app {
      min-height: 100%;
      display: flex;
      flex-direction: column;
    }
  
    .content {
      flex: 1;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  </style>
  