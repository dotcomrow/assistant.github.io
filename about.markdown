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
<!-- 
<form action="" method="POST" onsubmit="process(event)"> -->

<form id="verify" onsubmit="process(event)">
    <p>Enter your phone number:</p>
    <input id="phone" type="tel" name="phone" />
    <input type="submit" class="btn" value="Verify" />

    <label>
    <div class="alert alert-info" style="display: none"></div>
    <div class="alert alert-error" style="display: none"></div>
    </label>
</form>

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
    });

    // Define what happens in case of an error
    XHR.addEventListener("error", (event) => {
        alert("Oops! Something went wrong.");
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
