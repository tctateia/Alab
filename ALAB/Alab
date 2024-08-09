document.addEventListener('DOMContentLoaded', function () {
    const registrationForm = document.getElementById('registration');
    const loginForm = document.getElementById('login');
    const errorDisplay = document.getElementById('errorDisplay');

    function showError(message) {
        errorDisplay.style.display = 'flex';
        errorDisplay.textContent = message;
    }

    function hideError() {
        errorDisplay.style.display = 'none';
    }
    //lowercase letters no space capital letters numbers 0-9 references any character on the key board LC or Cap
    function validateUsername(username) {
        if (username.length < 4) return 'Username must be at least four characters long.';
        if (/[^a-zA-Z0-9]/.test(username)) return 'Username cannot contain special characters or whitespace.';
        const uniqueChars = new Set(username);
        if (uniqueChars.size < 2) return 'Username must contain at least two unique characters.';
    //do not understand json fully (look up codecademy lesson)
        const users = JSON.parse(localStorage.getItem('users') || '{}');
        if (users[username.toLowerCase()]) return 'That username is already taken.';
        return '';
    }

    function validateEmail(email) {
        const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        if (!emailRegex.test(email)) return 'Invalid email address.';
        if (email.endsWith('@example.com')) return 'Email cannot be from the domain "example.com".';
        return '';
    }
//stopped here password code next 
    function validatePassword(password, username) {
        if (password.length < 12) return 'Password must be at least 12 characters long.';
        if (!/[a-z]/.test(password) || !/[A-Z]/.test(password)) return 'Password must contain at least one uppercase and one lowercase letter.';
        if (!/\d/.test(password)) return 'Password must contain at least one number.';
        if (!/[!@#$%^&*(),.?":{}|<>]/.test(password)) return 'Password must contain at least one special character.';
        if (/password/i.test(password)) return 'Password cannot contain the word "password".';
        if (password.toLowerCase().includes(username.toLowerCase())) return 'Password cannot contain the username.';
        return '';
    }

    function registerUser(username, email, password) {
        const users = JSON.parse(localStorage.getItem('users') || '{}');
        users[username.toLowerCase()] = { email: email.toLowerCase(), password };
        localStorage.setItem('users', JSON.stringify(users));
    }

    registrationForm.addEventListener('submit', function (e) {
        e.preventDefault();
        hideError();

        const username = registrationForm.username.value.trim();
        const email = registrationForm.email.value.trim();
        const password = registrationForm.password.value;
        const passwordCheck = registrationForm.passwordCheck.value;

        let error = validateUsername(username);
        if (error) return showError(error);

        error = validateEmail(email);
        if (error) return showError(error);

        error = validatePassword(password, username);
        if (error) return showError(error);

        if (password !== passwordCheck) return showError('Passwords must match.');

        if (!registrationForm.terms.checked) return showError('You must agree to the terms and conditions.');

        registerUser(username, email, password);
        registrationForm.reset();
        showError('Registration successful!');
    });
    
    loginForm.addEventListener('submit', function (e) {
        e.preventDefault();
        hideError();

        const username = loginForm.username.value.trim().toLowerCase();
        const password = loginForm.password.value;

        const users = JSON.parse(localStorage.getItem('users') || '{}');
        if (!users[username]) return showError('Username does not exist.');
        if (users[username].password !== password) return showError('Incorrect password.');

        loginForm.reset();
        showError(loginForm.persist.checked ? 'Login successful! (persistent)' : 'Login successful!');
    });
     //parce this entire code. It works but not sure when it started working
});