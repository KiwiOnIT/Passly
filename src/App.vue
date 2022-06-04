<template>
<div class="box">
  <h1 class="title">Passly</h1>
  <p class="center">A simple password generator !</p>
    <div>
      <button value='Generate password'  class="btn center" v-on:click="this.generatePassword()">Generate</button>
      <p> </p>
      <input type="text"  id="inputText" v-model="password" class="password" readonly>
      <button  class="btnCopy" v-on:click="this.copy()">Copy</button>
      <p> </p>
      <input type="range" min="8" max="32" value="16" class="slider" id="myRange">
      <p>Length: <span id="length"></span></p>
    </div>

    <p> Made by <a  class="git-link" href="https://github.com/KiwiOnIT">KiwiIT</a> !</p>
</div>

</template>

<script>
export default {
      mounted() {
        this.generatePassword();
    },
    methods: {
       generatePassword() {
        var slider = document.getElementById("myRange");
        var output = document.getElementById("length");
        output.innerHTML = slider.value;
        slider.oninput = function() {
            output.innerHTML = this.value;
            var length = slider.value;
            var charset = '!@#$%^&*()_-+={[}]|:;"<,>.?/abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
            var retVal = "";
            for (var i = 0, n = charset.length; i < length; ++i) {
            retVal += charset.charAt(Math.floor(Math.random() * n));
            document.getElementById('inputText').value = retVal ;
        }      
        }
        var length = slider.value;
        var charset = '!@#$%^&*()_-+={[}]|:;"<,>.?/abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'
        var retVal = "";
        for (var i = 0, n = charset.length; i < length; ++i) {
            retVal += charset.charAt(Math.floor(Math.random() * n));
            document.getElementById('inputText').value = retVal 
        }      
      
    },
    copy() {
      var copyText = document.getElementById("inputText");
      copyText.select();
      copyText.setSelectionRange(0, 99999);
      navigator.clipboard.writeText(copyText.value);
      alert("Copied password: " + copyText.value);
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.title {
  margin-top: 70px;
}

.git-link {
  color: #00fa0c;
}
.box{
    color: rgb(250, 250, 250);
    width: 800px;
    min-height: 400px;
    padding: 20px;
    border-radius: 3px;
    height: auto;
    background: #393939;
    box-shadow: 0 10px 15px rgba(0,0,0,0.5);
    position: absolute;
    left: 50%;
    transform: translate(-50%);
    margin-top: 230px;
}
.btnCopy {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 3px 23px;
  text-align: center;
  text-decoration: none;
  font-size: 20px;
  border-radius: 2px;
  cursor: pointer;
  transition-duration: 0.4s;
}
.btn {
    background-color: #4CAF50;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    font-size: 24px;
    border-radius: 8px;
    cursor: pointer;
    transition-duration: 0.4s;
}
.btn:hover {
	background-color: rgb(18, 129, 3);
}
.password {
  font-size: 20px;
  margin-left: 10px;
}
.slider {
  -webkit-appearance: none;
  width: 25%;
  height: 15px;
  border-radius: 5px;  
  background: #d3d3d3;
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
  background: #4CAF50;
  cursor: pointer;
}
.slider::-moz-range-thumb {
  width: 25px;
  height: 25px;
  border-radius: 50%;
  background: #4CAF50;
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

@media screen and (max-width: 600px) {
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
}
</style>
