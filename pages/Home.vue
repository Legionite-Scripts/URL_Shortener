<template>
  <div class="home center p-2">
    <form class="center" ref="urlShortenerForm">
      <h1 class="mb-4">URL Shortener</h1>
      <input
        type="text"
        placeholder="Enter URL to be shortened (e.g https://example.com)"
        class="mb-3"
        ref="initialUrlInput"
      />
      <button type="submit" class="mb-2">Submit</button>
      <div v-if="shortLink">
        <a :href="shortLink" ref="shortenedLink" target="_blank">{{ shortLink }}</a>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      shortLink: '',
    }
  },

  mounted() {
    let form = this.$refs.urlShortenerForm //Identifying the form

    form.addEventListener('submit', async (e) => { //If a submit action is applied on the form
      e.preventDefault()
      let response = await fetch('https://url-shortener-yh27.onrender.com', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          long_url: this.$refs.initialUrlInput.value,
        }),
      })
      //If there is a bad response, console.log the response
      if (!response.ok) {
        console.log(response)
        return
      }
      let data = await response.json()
      console.log(data)
      this.shortLink = data.data.short_url // shortLink as a variable to the actual short URL
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
input::placeholder{
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

@media(max-width:1000px){
  form {
    width: 100vw;
  }
}
</style>
