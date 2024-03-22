<template>
  <div class="sidepanel p-1" ref="sidepanel">
    <div class="head text-center center mb-2">
      <h2 class="mt-2">Storage Preferences</h2>
      <span ref="close" @click="closePanel">&times;</span>
    </div>
    <p class="mb-1">
      When you visit websites, they may store or retrieve data about you using
      cookies and similar technologies ("cookies"). Cookies may be necessary for
      the basic functionality of the website as well as other purposes. You have
      the option of disabling certain types of cookies, though doing so may
      impact your experience on the website.
    </p>
    <a href="#" class="mb-2">Cookie Policy</a>

    <div class="head center mb-2">
      <h3>Essential</h3>

      <!-- Switch Button Slider -->
      <label class="switch">
        <input type="checkbox" />
        <span class="slider round"></span>
      </label>
    </div>
    <p class="mb-1">
      Required to enable basic website functionality. You may not disable
      essential cookies.
    </p>
    <a href="#" class="mb-2">View Cookies</a>
    <hr />

    <!-- Second Item -->
    <div class="head center mb-2 mt-2">
      <h3>Targeted Advertising</h3>

      <!-- Switch Button Slider -->
      <label class="switch">
        <input type="checkbox" />
        <span class="slider round"></span>
      </label>
    </div>
    <p class="mb-1">
      Used to deliver advertising that is more relevant to you and your
      interests. May also be used to limit the number of times you see an
      advertisement and measure the effectiveness of advertising campaigns.
      Advertising networks usually place them with the website operator’s
      permission.
    </p>
    <a href="#" class="mb-2">View Cookies</a>
    <hr />
    <!-- Third Item -->
    <div class="head center mb-2 mt-2">
      <h3>Personalization</h3>

      <!-- Switch Button Slider -->
      <label class="switch">
        <input type="checkbox" />
        <span class="slider round"></span>
      </label>
    </div>
    <p class="mb-1">
      Allow the website to remember choices you make (such as your username,
      language, or the region you are in) and provide enhanced, more personal
      features. For example, a website may provide you with local weather
      reports or traffic news by storing data about your general location.
    </p>
    <a href="#" class="mb-2">View Cookies</a>
    <hr />

    <!-- Fourth Item -->
    <div class="head center mb-2 mt-2">
      <h3>Analytics</h3>

      <!-- Switch Button Slider -->
      <label class="switch">
        <input type="checkbox" />
        <span class="slider round"></span>
      </label>
    </div>
    <p class="mb-1">
      Help the website operator understand how its website performs, how
      visitors interact with the site, and whether there may be technical
      issues.
    </p>
    <a href="#" class="mb-2">View Cookies</a>
    <hr />

    <a href="#" class="mt-3 mb-1"><button class="save">SAVE</button></a>
    <a href="#" class="center">Powered by Marv Magic</a>
  </div>
</template>

<script>
export default {
  methods: {
    closePanel() {
      // Access element using ref, not document.getElementById
      this.$refs.sidepanel.style.display = 'none'
    },
  },
}

//For the switch button slider
const switches = document.querySelectorAll('.switch')

switches.forEach((switchElement) => {
  const checkbox = switchElement.querySelector('input')
  const label = switchElement.textContent.trim()

  if (label) {
    checkbox.setAttribute('aria-label', label)
  }
})
</script>

<style scoped>
.sidepanel {
  height: 100vh;
  width: 20vw;
  display: flex;
  position: fixed;
  right: 0;
  flex-direction: column;
  overflow-y: auto;
  z-index: 1;
  border: 1px solid #333;
  background-color: #f8f8f8;
  transition: all .3s ease;
}

/* Switch Button Slider */
.switch {
  position: relative;
  display: inline-block;
  width: 60px;
  height: 34px;
  border-radius: 50px;
}

.switch input {
  opacity: 0;
  width: 0;
  height: 0;
  border-radius: 50px;
}

.slider {
  position: absolute;
  cursor: pointer;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: #ccc;
  transition: 0.4s;
  border-radius: 50px;
}

.slider:before {
  position: absolute;
  content: '';
  height: 26px;
  width: 26px;
  left: 4px;
  bottom: 4px;
  background-color: #fff;
  transition: 0.4s;
  border-radius: 50px;
}

input:checked + .slider {
  background-color: #37cd8f;
}

input:focus + .slider {
  box-shadow: 0 0 1px #ccc;
}

input:checked + .slider:before {
  transform: translateX(26px);
}
/* End */
.head {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
}
.sidepanel button.save {
  height: 4em !important;
  background-color: #260212;
  border: none;
  color: white;
  width: 100%;
}

span {
  font-size: 3em;
  font-weight: 300;
  cursor: pointer;
}

@media(max-width:1000px) 
{
  .sidepanel{
    width: 100vw;
  }
}
</style>
