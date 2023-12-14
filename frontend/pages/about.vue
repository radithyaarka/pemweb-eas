<template>
  <div class="flex flex-col min-h-screen">
    <div class="app">
      <Navbar />
      <anggota />
    </div>
    <Footer />
  </div>
  </template>
  
  <style>
    body, html {
      height: 100%;
      margin: 0;
      padding: 0;
      background-color:  #F7F7F7;
    }
  
    .app {
      min-height: 100%;
      display: flex;
      flex-direction: column;
    }
  
  </style>
  