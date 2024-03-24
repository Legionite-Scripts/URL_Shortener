<template>
  <div class="home center p-2">
    <form class="center" ref="urlShortenerForm">
      <h1 class="mb-4">URL Shortener</h1>
      <input
        type="text"
        placeholder="Enter URL to be shortened (e.g https://cool.com)"
        class="mb-3"
        ref="initialUrlInput"
      />
      <button type="submit" class="mb-2">Submit</button>
      <div v-if="shortLink">
        <a :href="shortLink" ref="shortenedLink" target="_blank">{{
          shortLink
        }}</a>
      </div>
      <div v-show="isLoading" class="loading-container">
        <div class="loading-icon"></div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      shortLink: '',
      isLoading: false, // New data property to control loading animation
    }
  },
  methods: {
    async submitForm() {
      this.isLoading = true // Show loading animation before fetch
      try {
        let response = await fetch('https://url-shortener-yh27.onrender.com', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            long_url: this.$refs.initialUrlInput.value,
          }),
        })
        if (!response.ok) {
          console.log(response)
          return
        }
        let data = await response.json()
        console.log(data)
        this.shortLink = data.data.short_url
      } catch (error) {
        console.error('Error fetching shortened URL:', error)
      } finally {
        this.isLoading = false // Hide loading animation after fetch completes
      }
    },
  },
  mounted() {
    let form = this.$refs.urlShortenerForm
    form.addEventListener('submit', (e) => {
      e.preventDefault()
      this.submitForm() // Call the new submitForm method
    })
  },
}
</script>

<style>
.home {
  height: 100vh;
  display: flex;
  justify-content: center;
}

form {
  width: 50vw;
}

input {
  width: 100%;
  height: 4em;
  border-radius: 10px;
  border: 1px solid #333;
  padding-left: 1em;
}

input::placeholder {
  font-size: 1.3em;
}

button {
  background-color: #101010;
  border: none;
  color: #ffffffff;
  border-radius: 50px;
  width: 15em;
  height: 3em;
  transition: all 0.3s ease;
}

button:hover {
  transform: scale(1.05);
}

.loading-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.3); /* Optional: Semi-transparent overlay */
  display: flex;
  justify-content: center;
  align-items: center;
}

.loading-icon {
  /* Add styles for your chosen loading animation here */
  width: 50px;
  height: 50px;
  border-radius: 50%;
  border: 5px solid #fff;
  border-top-color: transparent; /* Simulates spinning animation */
  animation: spin 1s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

@media (max-width: 1000px) {
  form {
    width: 100vw;
  }
  input::placeholder {
    font-size: 1em;
  }
}
</style>
