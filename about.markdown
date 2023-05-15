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
<form action="https://plib7qyexhoeljo2j6oye4e6oa0eyldb.lambda-url.us-east-1.on.aws/" method="POST" onsubmit="process(event)"> -->


<form id="verify" onsubmit="process(event)">
    <p>Enter your phone number:</p>
    <input id="phone" type="tel" name="phone" />
    <input type="submit" class="btn" value="Verify" />
</form>

<label>
<div class="alert alert-info" style="display: none"></div>
<div class="alert alert-error" style="display: none"></div>
</label>

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

 const data = new URLSearchParams();
 data.append("phone", phoneNumber);

const client = context.getTwilioClient();
const lookup = await client.lookups.v2.phoneNumbers(event.phone).fetch();

 if (lookup.valid) {
      response.setStatusCode(200);
      response.setBody({
        success: true,
      });
      callback(null, response);
    } else {
      response.setStatusCode(400);
      response.setBody({
        success: false,
        error: `Invalid phone number ${event.phone}: ${errorStr(
          lookup.validationErrors
        )}`,
      });
      callback(null, response);
    }
  } catch (error) {
    console.error(error);
    response.setStatusCode(error.status);
    response.setBody({
      success: false,
      error: "Something went wrong.",
    });
    callback(null, response);
  }
};
</script>
