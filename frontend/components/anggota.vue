<template>
  <div>
    <!-- Content -->
    <div class="display">
      <div class="content">
        <div class="tombol">
          <button @click="toggleTim">Dimana Aku?</button>
        </div>
        <div class="tim" v-if="showTim">
          <div class="card" v-for="(teamMember, index) in teamMembers" :key="index">
            <div class="card-details">
              <p class="text-title">{{ teamMember.name }}</p>
              <p class="text-body">{{ teamMember.nrp }}</p>
              <p class="text-body">{{ teamMember.description }}</p>
            </div>
            <button class="card-button" @click="openInstagramProfile(teamMember.instagram)">More info</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
  
<style scoped>
.display {
  display: flex;
  align-items: center;
  justify-content: center;
}

.content {
  display: flex;
  flex-direction: column;
  padding: 5vh;
  margin-top: 5vh;
  margin-bottom: 10vh;
  width: 70%;
  max-width: 80%;
  height: auto;
  max-height: 100vh;
  justify-content: center;
  align-items: center;
  box-sizing: border-box;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  position: relative;
}

.tombol {
  position: absolute;
  top: 1rem;
  left: 1rem;
}

.tim {
  display: flex;
  gap: 1rem; /* Add space between cards */
  margin-top: 7%;
  margin-bottom: 5%;
}

button {
  background-color: #fff;
  color: #000;
  border: 1px solid #000;
  border-radius: 10em;
  font-size: 17px;
  font-weight: 600;
  padding: 1em 2em;
  cursor: pointer;
  transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}

button:hover {
  transform: translateY(-4px) translateX(-2px);
  box-shadow: 2px 5px 0 0 #000;
}

button:active {
  transform: translateY(2px) translateX(1px);
  box-shadow: 0 0 0 0 #000;
}

.card {
  width: 250px;
  height: auto;
  border-radius: 20px;
  background: #f5f5f5;
  position: relative;
  padding: 1.8rem;
  border: 2px solid #c3c6ce;
  transition: 0.5s ease-out;
  overflow: visible;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 1rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.card-details {
  color: #000;
  gap: 0.5em;
  display: grid;
  place-content: center;
  margin-bottom: 1rem; /* Add margin to create space between text and button */
}

.card-button {
  width: 60%;
  border-radius: 1rem;
  border: none;
  background-color: #008bf8;
  color: #fff;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  /* Remove the 'position: absolute' and 'bottom: 1rem' properties */
  margin-top: 10px;
  align-self: center; /* Center the button horizontally */
  text-align: center; /* Center the text inside the button */
}
.text-body {
  color: #868686;
}

.text-title {
  font-size: 1.5em;
  font-weight: bold;
}

.card:hover {
  border-color: #008bf8;
  box-shadow: 0 4px 18px rgba(0, 0, 0, 0.25);
}

.card:hover .card-button {
  transform: translateY(-50%);
  opacity: 1;
}

footer {
  background-color: #123c69;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin-top: auto;
  width: 100%;
}
</style>

  
  <script>
export default {
  data() {
    return {
      showTim: false,
      teamMembers: [
        { name: 'Imam Nurhadi', description: 'Entry Fragger AyoBeliPiscok menggunakan Raze', nrp: '5027221046', instagram: 'ara_its'},
        { name: 'M. Arkananta R.T.', description: 'Smoker Idaman Bontang, sering marahin pengguna Raze karena nafsu', nrp: '5027221003', instagram: 'ara_its' },
        { name: 'Nur Aazka R.', description: 'KETUPEL GARPIT yang ngide beli pizza DOMINO', nrp: '5027221064', instagram: 'ara_its' },
      ],
    };
  },
  methods: {
    toggleTim() {
      this.showTim = !this.showTim;
    },
    openInstagramProfile(username) {
      // Assuming the Instagram username is provided in the 'username' parameter
      const url = `https://www.instagram.com/${username}/`;
      window.open(url, '_blank');
    },
  },
};
</script>