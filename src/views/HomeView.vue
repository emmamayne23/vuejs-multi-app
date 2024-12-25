<script setup></script>

<template>
  <main class="home-page">
    <div class="hero">
      <h1 class="font-semibold">Welcome to the Home Page</h1>
      <p>This is the main content of the home page.</p>
      <p>Visit the <RouterLink to="/task">Task</RouterLink> page to add tasks.</p>
      <p>
        Visit the <RouterLink to="/weather">Weather</RouterLink> page to get weather information.
      </p>
      <p>Visit the <RouterLink to="/movie">Movie</RouterLink> page to search for movies.</p>
    </div>
  </main>
</template>

<style scoped>
.home-page {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
  background-image: url('../assets/warm-bg.png');
  background-size: cover;
  background-position: center;
}

.hero {
  width: 90%;
  max-width: 600px;
  text-align: center;
  padding: 20px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
  font-size: 48px;
  margin-bottom: 20px;
  color: #333;
  text-shadow: 1px 1px 1px rgba(0, 0, 0, 0.2);
}

p {
  font-size: 24px;
  color: #666;
  margin-bottom: 10px;
}

a {
  color: #007bff;
  text-decoration: none;
  transition: color 0.3s ease;
}

a:hover {
  color: #0056b3;
}
</style>
