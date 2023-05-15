---
layout: page
title: Sign Up
permalink: /signup/
---

<script src="https://cdnjs.cloudflare.com/ajax/libs/intl-tel-input/17.0.8/js/intlTelInput.min.js"></script>
<link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/intl-tel-input/17.0.8/css/intlTelInput.css"
/>

<style>

.spanner{
  position:absolute;
  top: 50%;
  left: 0;
  background: #2a2a2a55;
  width: 100%;
  display:block;
  text-align:center;
  height: 300px;
  color: #FFF;
  transform: translateY(-50%);
  z-index: 1000;
  visibility: hidden;
}

.overlay{
  position: fixed;
	width: 100%;
	height: 100%;
  background: rgba(0,0,0,0.5);
  visibility: hidden;
}

.loader,
.loader:before,
.loader:after {
  border-radius: 50%;
  width: 2.5em;
  height: 2.5em;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  -webkit-animation: load7 1.8s infinite ease-in-out;
  animation: load7 1.8s infinite ease-in-out;
}
.loader {
  color: #ffffff;
  font-size: 10px;
  margin: 80px auto;
  position: relative;
  text-indent: -9999em;
  -webkit-transform: translateZ(0);
  -ms-transform: translateZ(0);
  transform: translateZ(0);
  -webkit-animation-delay: -0.16s;
  animation-delay: -0.16s;
}
.loader:before,
.loader:after {
  content: '';
  position: absolute;
  top: 0;
}
.loader:before {
  left: -3.5em;
  -webkit-animation-delay: -0.32s;
  animation-delay: -0.32s;
}
.loader:after {
  left: 3.5em;
}
@-webkit-keyframes load7 {
  0%,
  80%,
  100% {
    box-shadow: 0 2.5em 0 -1.3em;
  }
  40% {
    box-shadow: 0 2.5em 0 0;
  }
}
@keyframes load7 {
  0%,
  80%,
  100% {
    box-shadow: 0 2.5em 0 -1.3em;
  }
  40% {
    box-shadow: 0 2.5em 0 0;
  }
}

.show{
  visibility: visible;
}

.spanner, .overlay{
	opacity: 0;
	-webkit-transition: all 0.3s;
	-moz-transition: all 0.3s;
	transition: all 0.3s;
}

.spanner.show, .overlay.show {
	opacity: 1
}
</style>
<div class="wrapper">
<form id="verify" onsubmit="process(event)">
    <p>Enter your phone number:</p>
    <input id="phone" type="tel" name="phone" />
    <input type="submit" class="btn" value="Verify" />

    <label>
    <div class="alert alert-info" style="display: none"></div>
    <div class="alert alert-error" style="display: none"></div>
    </label>
</form>
</div>
<div class="overlay"></div>
<div class="spanner">
  <div class="loader"></div>
  <p>Registering Phone Number, Please Hold...</p>
</div>
<script>
    const phoneInputField = document.querySelector("#phone");
    const phoneInput = window.intlTelInput(phoneInputField, {
      utilsScript:
        "https://cdnjs.cloudflare.com/ajax/libs/intl-tel-input/17.0.8/js/utils.js",
    });

    const info = document.querySelector(".alert-info");
    const error = document.querySelector(".alert-error");

function process(event) {
 event.preventDefault();
 document.querySelector("div.spanner").classList.add("show");
 document.querySelector("div.overlay").classList.add("show");
 const phoneNumber = phoneInput.getNumber();

 info.style.display = "none";
 error.style.display = "none";

 if (phoneInput.isValidNumber()) {
    info.style.display = "";
    info.innerHTML = "";

    console.log("Sending data");

    data = {
        "phoneNumber":phoneNumber
    };
    const XHR = new XMLHttpRequest();

    const urlEncodedDataPairs = [];

    // Turn the data object into an array of URL-encoded key/value pairs.
    for (const [name, value] of Object.entries(data)) {
        urlEncodedDataPairs.push(
            `${encodeURIComponent(name)}=${encodeURIComponent(value)}`
        );
    }

    // Combine the pairs into a single string and replace all %-encoded spaces to
    // the '+' character; matches the behavior of browser form submissions.
    const urlEncodedData = urlEncodedDataPairs.join("&").replace(/%20/g, "+");

    // Define what happens on successful data submission
    XHR.addEventListener("load", (event) => {
        alert("Yeah! Data sent and response loaded.");
        //document.querySelector("div.spanner").classList.remove("show");
        //document.querySelector("div.overlay").classList.remove("show");
    });

    // Define what happens in case of an error
    XHR.addEventListener("error", (event) => {
        alert("Oops! Something went wrong.");
        document.querySelector("div.spanner").classList.remove("show");
        document.querySelector("div.overlay").classList.remove("show");
    });

    // Set up our request
    XHR.open("POST", "https://plib7qyexhoeljo2j6oye4e6oa0eyldb.lambda-url.us-east-1.on.aws/");

    // Add the required HTTP header for form data POST requests
    XHR.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
    // Finally, send our data.
    XHR.send(urlEncodedData);
} else {
   error.style.display = "";
   error.innerHTML = `Invalid phone number.`;
}
}
</script>
