Objective:
Build a functional webpage that incorporates event handling, interactive elements, and form validation using JavaScript.

Requirements:
Interactive Button with onclick:

Add a button that toggles the background color of the webpage between two colors. Slider with Real-Time Feedback (oninput):

Add a slider that adjusts the size of a paragraph text dynamically. Modal with Event Listeners:

Create a modal that displays when a button is clicked and hides when the user clicks a close button.

Form with Validation:
Include a form with the following fields: Name (required, minimum 3 characters). Email (valid email format). Password (minimum 8 characters, at least one uppercase letter and one number). Display error messages if validation fails. Prevent form submission if there are errors. Bonus (Optional):

Add a dropdown menu that displays a custom message when the selected option changes (onchange).

# Week-3-day-6-assignment-
My assignment for week 3day 6

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Interactive Webpage</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      transition: background-color 0.3s;
      margin: 20px;
    }

    #sliderValue {
      font-weight: bold;
    }

    .hidden {
      display: none;
    }

    #modal {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      width: 300px;
      padding: 20px;
      background: white;
      box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.3);
      z-index: 1000;
    }

    #modalOverlay {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: rgba(0, 0, 0, 0.5);
      z-index: 999;
    }

    form div {
      margin-bottom: 15px;
    }

    .error {
      color: red;
      font-size: 0.9em;
    }
  </style>
</head>
<body>
  <button onclick="toggleBackground()">Toggle Background</button>
  <p>Adjust text size using the slider: <span id="sliderValue">16</span>px</p>
  <input type="range" id="textSlider" min="12" max="36" value="16" oninput="adjustTextSize()" />
  <p id="resizableText">This is resizable text.</p>

  <button onclick="showModal()">Open Modal</button>
  <div id="modalOverlay" class="hidden"></div>
  <div id="modal" class="hidden">
    <p>This is a modal!</p>
    <button onclick="closeModal()">Close</button>
  </div>

  <h2>Form with Validation</h2>
  <form id="form">
    <div>
      <label for="name">Name:</label>
      <input type="text" id="name" />
      <div id="nameError" class="error"></div>
    </div>
    <div>
      <label for="email">Email:</label>
      <input type="email" id="email" />
      <div id="emailError" class="error"></div>
    </div>
    <div>
      <label for="password">Password:</label>
      <input type="password" id="password" />
      <div id="passwordError" class="error"></div>
    </div>
    <button type="submit">Submit</button>
  </form>

  <h2>Dropdown Menu</h2>
  <select id="dropdown" onchange="displayDropdownMessage()">
    <option value="">Select an option</option>
    <option value="option1">Option 1</option>
    <option value="option2">Option 2</option>
  </select>
  <p id="dropdownMessage"></p>

  <script src="script.js"></script>
</body>
</html>

// Toggle Background Color
let isBlue = false;
function toggleBackground() {
  document.body.style.backgroundColor = isBlue ? "white" : "#add8e6";
  isBlue = !isBlue;
}

// Adjust Text Size
function adjustTextSize() {
  const slider = document.getElementById("textSlider");
  const text = document.getElementById("resizableText");
  const sliderValue = document.getElementById("sliderValue");
  text.style.fontSize = slider.value + "px";
  sliderValue.textContent = slider.value;
}

// Modal Event Handling
function showModal() {
  document.getElementById("modal").classList.remove("hidden");
  document.getElementById("modalOverlay").classList.remove("hidden");
}

function closeModal() {
  document.getElementById("modal").classList.add("hidden");
  document.getElementById("modalOverlay").classList.add("hidden");
}

// Form Validation
document.getElementById("form").addEventListener("submit", function (e) {
  let isValid = true;

  // Name Validation
  const name = document.getElementById("name").value;
  const nameError = document.getElementById("nameError");
  if (name.length < 3) {
    nameError.textContent = "Name must be at least 3 characters.";
    isValid = false;
  } else {
    nameError.textContent = "";
  }

  // Email Validation
  const email = document.getElementById("email").value;
  const emailError = document.getElementById("emailError");
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  if (!emailRegex.test(email)) {
    emailError.textContent = "Invalid email format.";
    isValid = false;
  } else {
    emailError.textContent = "";
  }

  // Password Validation
  const password = document.getElementById("password").value;
  const passwordError = document.getElementById("passwordError");
  const passwordRegex = /^(?=.*[A-Z])(?=.*\d).{8,}$/;
  if (!passwordRegex.test(password)) {
    passwordError.textContent =
      "Password must be at least 8 characters, including 1 uppercase letter and 1 number.";
    isValid = false;
  } else {
    passwordError.textContent = "";
  }

  if (!isValid) e.preventDefault();
});

// Dropdown Message
function displayDropdownMessage() {
  const dropdown = document.getElementById("dropdown");
  const message = document.getElementById("dropdownMessage");
  if (dropdown.value === "option1") {
    message.textContent = "You selected Option 1!";
  } else if (dropdown.value === "option2") {
    message.textContent = "You selected Option 2!";
  } else {
    message.textContent = "";
  }
}
