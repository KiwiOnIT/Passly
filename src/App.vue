<template>
  <div class="box">
    <h1 class="title">Passly</h1>
    <div id="password" v-text="password" class="password in-box"></div>
    <p>Length: <span id="length" v-text="length"></span></p>
    <div class="in-box">
      <input type="range" min="8" max="32" value="20" class="slider" id="myRange">
    </div>
    <p>Settings:</p>

    <div class="in-box d-flex" style="align-items: center;">
      <p class="settings-text" style="flex: 1; text-align: left;">Include uppercase characters</p>
      <label class="toggler-wrapper style-4" style="flex: 0 0 auto; text-align: left; display: inline-block; margin-right: 25px;">
          <input type="checkbox" v-model="includeUppercase">
          <div class="toggler-slider">
            <div class="toggler-knob"></div>
          </div>
        </label>
    </div>
      <br>
      <div class="in-box d-flex" style="align-items: center;">
        <p class="settings-text" style="flex: 1; text-align: left;">Include lowercase characters</p>
        <label class="toggler-wrapper style-4" style="flex: 0 0 auto; text-align: left; display: inline-block; margin-right: 25px;">
          <input type="checkbox" v-model="includeLowercase">
          <div class="toggler-slider">
            <div class="toggler-knob"></div>
          </div>
        </label>
      </div>
      <br>
      <div class="in-box d-flex" style="align-items: center;">
        <p class="settings-text" style="flex: 1; text-align: left;">Include special characters</p>
        <label class="toggler-wrapper style-4" style="flex: 0 0 auto; text-align: left; display: inline-block; margin-right: 25px;">
          <input type="checkbox" v-model="includeSpecialCharacters">
          <div class="toggler-slider">
            <div class="toggler-knob"></div>
          </div>
        </label>
      </div>
      <br>
      <div class="in-box d-flex" style="align-items: center;">
        <p class="settings-text" style="flex: 1; text-align: left;">Include numbers</p>
        <label class="toggler-wrapper style-4" style="flex: 0 0 auto; text-align: left; display: inline-block; margin-right: 25px;">
          <input type="checkbox" v-model="includeNumbers">
          <div class="toggler-slider">
            <div class="toggler-knob"></div>
          </div>
        </label>
      </div>
    <br>
    <button value='Generate password' class="btn center" v-on:click="generatePassword">Generate</button>
    <div class="center">
      <p> Made by <a class="git-link" href="https://github.com/KiwiOnIT">KiwiIT</a> !</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      includeUppercase: true,
      includeLowercase: true,
      includeSpecialCharacters: true,
      includeNumbers: true,
      password: '',
      length: 20,
    };
  },
  mounted() {
    var slider = document.getElementById("myRange");
    var output = document.getElementById("length");
    if (output) {
      output.innerHTML = slider.value;
    }
    slider.oninput = (event) => {
      if (output) {
        output.innerHTML = event.target.value;
      }
      this.length = event.target.value;
      this.generatePassword();
    };
    this.generatePassword();
  },
  methods: {
    generatePassword() {
      var length = this.length;
      var charset = '';
      if (this.includeUppercase) {
        charset += 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
      }
      if (this.includeLowercase) {
        charset += 'abcdefghijklmnopqrstuvwxyz';
      }
      if (this.includeSpecialCharacters) {
        charset += '!@#$%^&*()_-+={[}]|:;"<,>.?/';
      }
      if (this.includeNumbers) {
        charset += '0123456789';
      }
      var retVal = '';
      for (var i = 0, n = charset.length; i < length; ++i) {
        retVal += charset.charAt(Math.floor(Math.random() * n));
      }
      this.password = retVal;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
}

.title {
  margin-top: 20px;
  font-size: 1.75rem;
}

.git-link {
  color: rgb(11, 241, 107);
}
.box{
    color: rgb(250, 250, 250);
    width: 20vw;
    min-height: 60vh;
    padding: 20px;
    border-radius: 10px;
    height: auto;
    background: #2b2b2b;
    box-shadow: rgba(0, 0, 0, 0.56) 0px 22px 70px 4px;
    position: absolute;
    left: 50%;
    transform: translate(-50%);
    margin-top: 7vh;
    padding: 10px 25px;
}

.password {
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  color: #fff;
  text-align: center;
  line-height: 65px;
}
.slider {
  -webkit-appearance: none;
  width: 80%;
  height: 2px;
  border-radius: 5px;  
  background: whitesmoke;
  outline: none;
  opacity: 0.7;
  -webkit-transition: .2s;
  transition: opacity .2s;
}
.slider::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 25px;
  height: 25px;
  border-radius: 50%; 
  background: rgb(11, 241, 107);
  cursor: pointer;
}
.slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background: rgb(11, 241, 107);
  cursor: pointer;
}
body {
  background-color: #2b2b2b;
}
.center {
  margin-left: auto;
  margin-right: auto;
  display: flex;
  justify-content: center;
}

@media screen and (max-width: 1000px) {
  .box {
    width: 75%;
    margin-top: 150px;
  }
  .slider {
    width: 70%;
  }

  .btn {
    font-size: 16px;
  }
  .password {
    font-size: 16px;
    width: 50%;
  }
}

.btn{
  background-color: rgb(11, 241, 107);
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  width: 100%;
  height: 100%;
  border-radius: 10px;
  font-size: 24px;
}

.btn:hover {
  background-color: rgb(0, 222, 92);
}

.in-box{
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.08);
  border-radius: 8px;
  color: #fff;
  text-align: center;
  line-height: 50px;
}

.toggler-wrapper {
    display: block;
    width: 45px;
    height: 25px;
    cursor: pointer;
    position: relative;
}

.toggler-wrapper input[type="checkbox"] {
    display: none;
}

.toggler-wrapper input[type="checkbox"]:checked+.toggler-slider {
    background-color: #44cc66;
}

.toggler-wrapper .toggler-slider {
    background-color: #ccc;
    position: absolute;
    border-radius: 100px;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    -webkit-transition: all 300ms ease;
    transition: all 300ms ease;
}

.toggler-wrapper .toggler-knob {
    position: absolute;
    -webkit-transition: all 300ms ease;
    transition: all 300ms ease;
}
.toggler-wrapper.style-4 input[type="checkbox"]:checked+.toggler-slider .toggler-knob {
    left: calc(100% - 19px - 3px);
}

.toggler-wrapper.style-4 .toggler-knob {
    width: 25px;
    height: 25px;
    border-radius: 50%;
    left: 0;
    top: 0;
    background-color: #fff;
    -webkit-box-shadow: 0 2px 6px rgba(153, 153, 153, 0.75);
    box-shadow: 0 2px 6px rgba(153, 153, 153, 0.75);
}

.d-flex{
  display: flex;
}

.settings-text{
  margin-left: 25px;
}
</style>  
