<!DOCTYPE html>
<html lang="fi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Talviteemainen Sivu</title>
    <style>
        body {
            background: linear-gradient(-45deg, #1e3c72, #2a5298, #1e3c72, #2a5298);
            background-size: 400% 400%;
            animation: gradient 15s ease infinite;
            color: #fff;
            font-family: Arial, sans-serif;
            text-align: center;
            padding: 50px;
            overflow: hidden;
        }
        @keyframes gradient {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }
        .snowflake {
            color: #fff;
            font-size: 2em;
            position: absolute;
            top: -10%;
            z-index: 9999;
            user-select: none;
            pointer-events: none;
            animation: fall linear infinite;
        }
        @keyframes fall {
            0% { transform: translateY(0); }
            100% { transform: translateY(100vh); }
        }
        .button-container {
            margin-top: 20px;
        }
        .button {
            background-color: #007bff;
            border: none;
            color: white;
            padding: 15px 32px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 4px 2px;
            cursor: pointer;
            border-radius: 4px;
            transition: background-color 0.3s ease;
        }
        .button:hover {
            background-color: #0056b3;
        }
        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        .footer {
            margin-top: 50px;
            font-size: 0.8em;
            color: #aaa;
        }
        .top-right {
            position: absolute;
            top: 10px;
            right: 10px;
        }
        .top-right .button {
            padding: 10px 20px;
            font-size: 14px;
        }
        .top-left {
            position: absolute;
            top: 10px;
            left: 10px;
            font-size: 14px;
        }
        .modal {
            display: none;
            position: fixed;
            z-index: 10000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0, 0, 0, 0.5);
        }
        .modal-content {
            background-color: #fff;
            margin: 15% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 80%;
            max-width: 400px;
            color: #000;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
        }
        .close:hover,
        .close:focus {
            color: black;
            text-decoration: none;
            cursor: pointer;
        }
        .modal-content form {
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        .modal-content label {
            margin: 10px 0 5px;
            font-weight: bold;
        }
        .modal-content input {
            padding: 10px;
            width: 80%;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .modal-content button {
            background-color: #007bff;
            border: none;
            color: white;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s ease;
        }
        .modal-content button:hover {
            background-color: #0056b3;
        }
        .info-box {
            border: 2px solid #fff;
            padding: 20px;
            margin-top: 20px;
            border-radius: 10px;
            max-width: 800px;
            margin: 20px auto;
            background: rgba(255, 255, 255, 0.1);
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
        }
    </style>
</head>
<body>
    <div class="top-left" id="userStatus">
        LOGGED IN: <span id="usernameDisplay">Not logged in</span>
    </div>
    <div class="top-right">
        <button class="button" id="registerBtn">Register</button>
        <button class="button" id="loginBtn">Login</button>
    </div>
    <div class="container">
        <h1>WELCOME TO DIA LEAKS</h1>
        <div class="button-container">
            <a href="https://discord.gg/ARYqTkDDGW" class="button">DISCORD</a>
        </div>
    </div>
    <div class="info-box">
        <p>Welcome to the Dia Leaks website. From here you can join our Discord. Create a ticket if you are interested in leaking all kinds of information to us. Thank you!</p>
    </div>
    <div class="footer">
        <p>&copy; 2023 Talviteemainen Sivu. All rights reserved.</p>
    </div>

    <div id="registerModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>Register</h2>
            <form id="registerForm">
                <label for="regUsername">Username:</label>
                <input type="text" id="regUsername" name="regUsername">
                <label for="regPassword">Password:</label>
                <input type="password" id="regPassword" name="regPassword">
                <button type="submit" class="button">Register</button>
            </form>
        </div>
    </div>

    <div id="loginModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <h2>Login</h2>
            <form id="loginForm">
                <label for="username">Username:</label>
                <input type="text" id="username" name="username">
                <label for="password">Password:</label>
                <input type="password" id="password" name="password">
                <button type="submit" class="button">Login</button>
            </form>
        </div>
    </div>

    <script>
        function createSnowflake() {
            const snowflake = document.createElement('div');
            snowflake.classList.add('snowflake');
            snowflake.textContent = '❄';
            snowflake.style.left = Math.random() * 100 + 'vw';
            snowflake.style.animationDuration = Math.random() * 3 + 2 + 's';
            document.body.appendChild(snowflake);
            setTimeout(() => {
                snowflake.remove();
            }, 5000);
        }
        setInterval(createSnowflake, 300);

        const registerModal = document.getElementById("registerModal");
        const loginModal = document.getElementById("loginModal");
        const registerBtn = document.getElementById("registerBtn");
        const loginBtn = document.getElementById("loginBtn");
        const closeButtons = document.getElementsByClassName("close");
        const registerForm = document.getElementById("registerForm");
        const loginForm = document.getElementById("loginForm");
        const usernameDisplay = document.getElementById("usernameDisplay");

        let registeredUsers = {};

        registerBtn.onclick = function() {
            registerModal.style.display = "block";
        }

        loginBtn.onclick = function() {
            loginModal.style.display = "block";
        }

        for (let i = 0; i < closeButtons.length; i++) {
            closeButtons[i].onclick = function() {
                registerModal.style.display = "none";
                loginModal.style.display = "none";
            }
        }

        window.onclick = function(event) {
            if (event.target == registerModal) {
                registerModal.style.display = "none";
            }
            if (event.target == loginModal) {
                loginModal.style.display = "none";
            }
        }

        registerForm.onsubmit = function(event) {
            event.preventDefault();
            const regUsername = document.getElementById("regUsername").value;
            const regPassword = document.getElementById("regPassword").value;
            registeredUsers[regUsername] = regPassword;
            registerModal.style.display = "none";
            alert("Registration successful! You can now log in.");
        }

        loginForm.onsubmit = function(event) {
            event.preventDefault();
            const username = document.getElementById("username").value;
            const password = document.getElementById("password").value;
            if (registeredUsers[username] && registeredUsers[username] === password) {
                usernameDisplay.textContent = username;
                loginModal.style.display = "none";
            } else {
                alert("Invalid username or password.");
            }
        }
    </script>
</body>
</html>
