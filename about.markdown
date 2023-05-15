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
<script>
    const phoneInputField = document.querySelector("#phoneNumber");
    const phoneInput = window.intlTelInput(phoneInputField, {
      utilsScript:
        "https://cdnjs.cloudflare.com/ajax/libs/intl-tel-input/17.0.8/js/utils.js",
    });

    const info = document.querySelector(".alert-info");
    const error = document.querySelector(".alert-error");

    function process(event) {
      event.preventDefault();

      const phoneNumber = phoneInput.getNumber();

      info.style.display = "";
      info.innerHTML = `Phone number in E.164 format: <strong>${phoneNumber}</strong>`;
    }
  </script>

<form action="https://plib7qyexhoeljo2j6oye4e6oa0eyldb.lambda-url.us-east-1.on.aws/" method="POST" onsubmit="process(event)">

<label>
First Name : <input type="text" name="firstName" id="firstName"/>
</label>

<label>
Last Name : <input type="text" name="lastName" id="lastName"/>
</label>
<input type="submit"/>
</form>
      <form id="login" onsubmit="process(event)">
        <p>Enter your phone number:</p>
        <input id="phone" type="tel" name="phone" />
        <input type="submit" class="btn" value="Verify" />
      </form><label>
      <div class="alert alert-info" style="display: none"></div>
      <div class="alert alert-error" style="display: none"></div>
</label>
