<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Webpage</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
        }
        #modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background-color: white;
            padding: 20px;
            border-radius: 5px;
        }
        .error {
            color: red;
            font-size: 12px;
        }
    </style>
</head>
<body>

    <h1>Interactive Webpage</h1>

    <!-- Button to toggle background color -->
    <button onclick="toggleBackgroundColor()">Toggle Background Color</button>

    <!-- Slider to adjust text size -->
    <div>
        <label for="textSizeSlider">Adjust Text Size: </label>
        <input type="range" id="textSizeSlider" min="10" max="50" value="16" oninput="adjustTextSize(this.value)">
        <span id="textSizeValue">16px</span>
    </div>

    <!-- Modal Button -->
    <button onclick="openModal()">Open Modal</button>

    <!-- Modal -->
    <div id="modal">
        <div class="modal-content">
            <span onclick="closeModal()" style="cursor: pointer;">&times; Close</span>
            <p>This is a modal. Click "Close" to hide it.</p>
        </div>
    </div>

    <!-- Form for validation -->
    <form id="myForm" onsubmit="return validateForm()">
        <h2>Sign Up</h2>
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required minlength="3"><br>
        <div id="nameError" class="error"></div>

        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required><br>
        <div id="emailError" class="error"></div>

        <label for="password">Password:</label>
        <input type="password" id="password" name="password" required minlength="8"><br>
        <div id="passwordError" class="error"></div>

        <button type="submit">Submit</button>
    </form>

    <!-- Bonus: Dropdown menu -->
    <div>
        <label for="dropdown">Select an option: </label>
        <select id="dropdown" onchange="displayDropdownMessage(this)">
            <option value="">Select...</option>
            <option value="Option 1">Option 1</option>
            <option value="Option 2">Option 2</option>
            <option value="Option 3">Option 3</option>
        </select>
        <p id="dropdownMessage"></p>
    </div>

    <script>
        // Toggle background color
        function toggleBackgroundColor() {
            const currentColor = document.body.style.backgroundColor;
            if (currentColor === 'lightblue') {
                document.body.style.backgroundColor = 'lightgreen';
            } else {
                document.body.style.backgroundColor = 'lightblue';
            }
        }

        // Adjust text size with slider
        function adjustTextSize(size) {
            document.getElementById("textSizeValue").textContent = size + "px";
            document.body.style.fontSize = size + "px";
        }

        // Open Modal
        function openModal() {
            document.getElementById("modal").style.display = "flex";
        }

        // Close Modal
        function closeModal() {
            document.getElementById("modal").style.display = "none";
        }

        // Form Validation
        function validateForm() {
            let isValid = true;

            // Clear previous error messages
            document.getElementById("nameError").textContent = "";
            document.getElementById("emailError").textContent = "";
            document.getElementById("passwordError").textContent = "";

            const name = document.getElementById("name").value;
            const email = document.getElementById("email").value;
            const password = document.getElementById("password").value;

            // Validate Name
            if (name.length < 3) {
                document.getElementById("nameError").textContent = "Name must be at least 3 characters long.";
                isValid = false;
            }

            // Validate Email
            const emailPattern = /^[a-zA-Z0-9._-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,6}$/;
            if (!emailPattern.test(email)) {
                document.getElementById("emailError").textContent = "Please enter a valid email address.";
                isValid = false;
            }

            // Validate Password
            const passwordPattern = /^(?=.*[A-Z])(?=.*\d)[A-Za-z\d]{8,}$/;
            if (!passwordPattern.test(password)) {
                document.getElementById("passwordError").textContent = "Password must be at least 8 characters long, with at least one uppercase letter and one number.";
                isValid = false;
            }

            return isValid; // Prevent form submission if validation fails
        }

        // Dropdown change event
        function displayDropdownMessage(select) {
            const message = "You selected: " + select.value;
            document.getElementById("dropdownMessage").textContent = message;
        }
    </script>
</body>
</html>
