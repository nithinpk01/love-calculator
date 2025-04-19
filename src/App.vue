<template>
  <div class="container">
    <div class="form-container">
      <h1 class="title">💘 Love Calculator 💘</h1>

      <div class="form">
        <div class="input-group">
          <input
            v-model="name1"
            type="text"
            placeholder="Your Name"
            class="input"
          />
        </div>

        <div class="input-group">
          <input
            v-model="name2"
            type="text"
            placeholder="Crush's Name"
            class="input"
          />
        </div>

        <button class="button" @click="calculateLove">
          💖 Calculate 💖
        </button>

        <!-- Custom Notification -->
        <div v-if="showNotification" class="notification">
          <p>Please enter both names!</p>
        </div>

        <div v-if="result !== null" class="result">
          <p class="match">
            Love Match:
            <span class="percentage">{{ result }}%</span>
          </p>
          <p class="message">{{ message }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const name1 = ref('')
const name2 = ref('')
const result = ref(null)
const message = ref('')
const showNotification = ref(false)

function calculateLove() {
  if (name1.value.trim() === '' || name2.value.trim() === '') {
    showNotification.value = true
    setTimeout(() => {
      showNotification.value = false
    }, 3000) // Hide after 3 seconds
    return
  }

  const combined = name1.value.trim().toLowerCase() + name2.value.trim().toLowerCase()
  let score = 0
  for (let i = 0; i < combined.length; i++) {
    score += combined.charCodeAt(i)
  }
  const loveScore = score % 101
  result.value = loveScore

  if (loveScore > 80) {
    message.value = "A match made in heaven! 💞"
  } else if (loveScore > 60) {
    message.value = "You two are pretty compatible! "
  } else if (loveScore > 40) {
    message.value = "There’s potential here! 💌"
  } else {
    message.value = "Hmm... maybe just friends? 💔"
  }
}
</script>

<style scoped>
/* General Styles */
body {
  margin: 0;
  padding: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: linear-gradient(to bottom right, #ffb6c1, #f06292);
  padding: 20px;
}

.form-container {
  width: 100%;
  max-width: 600px;
  text-align: center;
  background: white;
  border-radius: 24px;
  padding: 40px;
  box-shadow: 0 8px 15px rgba(0, 0, 0, 0.1);
}

.title {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 20px;
  text-shadow: 2px 2px 8px rgba(0, 0, 0, 0.2);
  background: linear-gradient(to right, #ff4081, #9c27b0); /* Gradient background */
  -webkit-background-clip: text;
  color: transparent; /* Makes text transparent to show the gradient */
}

.title {
  color: #333333; /* Dark color for better visibility */
  text-shadow: 4px 4px 10px rgba(0, 0, 0, 0.5); /* Adds more contrast */
}


.form {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

/* Input Fields */
.input-group {
  width: 100%;
}

.input {
  width: 100%;
  padding: 15px;
  border: 2px solid #f06292;
  border-radius: 20px;
  font-size: 1.1rem;
  background-color: #f8bbd0;
  color: #d81b60;
  transition: all 0.3s ease;
}

.input:focus {
  border-color: #f50057;
  outline: none;
  box-shadow: 0 0 5px 2px rgba(244, 0, 87, 0.4);
}

.input::placeholder {
  color: #d81b60;
  font-style: italic;
}

/* Button */
.button {
  padding: 15px 30px;
  font-size: 1.2rem;
  font-weight: bold;
  background: linear-gradient(to right, #f06292, #ff4081);
  color: white;
  border-radius: 30px;
  border: none;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
}

.button:hover {
  background: linear-gradient(to right, #f50057, #ff1744);
  transform: scale(1.05);
}

.button:active {
  transform: scale(0.98);
}

/* Notification */
.notification {
  background-color: #ff1744;
  color: white;
  font-size: 1.1rem;
  padding: 12px 20px;
  border-radius: 12px;
  margin-top: 20px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  animation: fadeIn 1s ease-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(-20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}

/* Result Styling */
.result {
  margin-top: 30px;
}

.match {
  font-size: 1.5rem;
  font-weight: bold;
  color: #424242;
}

.percentage {
  color: #f50057;
  animation: bounce 1s infinite;
}

.message {
  font-size: 1.1rem;
  color: #757575;
  font-style: italic;
}

/* Keyframe for bounce effect */
@keyframes bounce {
  0%, 20%, 40%, 60%, 80%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

/* Mobile Responsiveness */
@media (max-width: 768px) {
  .title {
    font-size: 2rem; /* Smaller font size on mobile */
    margin-bottom: 15px;
  }

  .form-container {
    padding: 30px;
  }

  .input {
    font-size: 1rem; /* Smaller font size on inputs */
    padding: 12px;
  }

  .button {
    font-size: 1.1rem;
    padding: 12px 25px;
  }

  .match {
    font-size: 1.2rem;
  }

  .message {
    font-size: 1rem;
  }
}

@media (max-width: 480px) {
  .title {
    font-size: 1.8rem; /* Further reduce font size for very small screens */
    margin-bottom: 10px;
  }

  .input {
    font-size: 0.9rem;
    padding: 10px;
  }

  .button {
    font-size: 1rem;
    padding: 10px 20px;
  }

  .match {
    font-size: 1.1rem;
  }

  .message {
    font-size: 0.9rem;
  }
}
</style>
