<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Azure DevOps Portal | Login & Registration</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            margin: 0;
            font-family: "Segoe UI", -apple-system, BlinkMacSystemFont, Roboto, sans-serif;
            background: linear-gradient(135deg, #0f172a, #1e293b, #312e81);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 2rem 1rem;
        }

        /* main card container - handles both pages */
        .auth-container {
            width: 100%;
            max-width: 500px;
            background: #ffffff;
            border-radius: 28px;
            box-shadow: 0 25px 45px -12px rgba(0, 0, 0, 0.45), 0 4px 12px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            transition: all 0.2s ease;
        }

        /* header with toggle controls */
        .auth-header {
            display: flex;
            background: #f8fafc;
            border-bottom: 1px solid #e2e8f0;
        }

        .tab-btn {
            flex: 1;
            text-align: center;
            padding: 1rem 0;
            font-weight: 700;
            font-size: 1.1rem;
            cursor: pointer;
            background: transparent;
            border: none;
            transition: all 0.2s;
            color: #475569;
            letter-spacing: 0.3px;
        }

        .tab-btn.active {
            color: #0078d4;
            background: white;
            border-bottom: 3px solid #0078d4;
            box-shadow: 0 -2px 5px rgba(0,120,212,0.05);
        }

        .tab-btn:first-child.active {
            border-radius: 28px 0 0 0;
        }
        .tab-btn:last-child.active {
            border-radius: 0 28px 0 0;
        }

        .form-pane {
            padding: 2rem 1.8rem 2rem 1.8rem;
            display: none;
            animation: fadeSlide 0.25s ease-out;
        }

        .form-pane.active-pane {
            display: block;
        }

        @keyframes fadeSlide {
            from {
                opacity: 0;
                transform: translateY(8px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        h2 {
            text-align: center;
            color: #0a2540;
            font-weight: 600;
            font-size: 1.7rem;
            margin-bottom: 1.5rem;
            letter-spacing: -0.3px;
        }

        /* unified field styles */
        .field-group {
            margin-bottom: 1.2rem;
        }

        label {
            font-weight: 600;
            font-size: 0.85rem;
            color: #1e293b;
            display: block;
            margin-bottom: 0.25rem;
        }

        input, textarea {
            width: 100%;
            padding: 12px 14px;
            border-radius: 14px;
            border: 2px solid #e2e8f0;
            outline: none;
            transition: 0.2s;
            background: #ffffff;
            font-size: 0.95rem;
            font-family: inherit;
        }

        input:focus, textarea:focus {
            border-color: #0078d4;
            box-shadow: 0 0 0 3px rgba(0,120,212,0.2);
        }

        .valid {
            border: 2px solid #22c55e;
            background-color: #f0fdf4;
        }

        .invalid {
            border: 2px solid #ef4444;
            background-color: #fef2f2;
        }

        .error {
            color: #ef4444;
            font-size: 0.7rem;
            margin-top: 4px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        .successText {
            color: #22c55e;
            font-size: 0.7rem;
            margin-top: 4px;
            font-weight: 500;
            display: flex;
            align-items: center;
            gap: 4px;
        }

        button[type="submit"], .action-btn {
            width: 100%;
            padding: 12px;
            margin-top: 12px;
            border: none;
            border-radius: 40px;
            background: linear-gradient(90deg, #0078d4, #106ebe);
            color: white;
            font-size: 1rem;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
            box-shadow: 0 4px 8px rgba(0,0,0,0.05);
        }

        button[type="submit"]:hover, .action-btn:hover {
            transform: scale(1.01);
            background: linear-gradient(90deg, #106ebe, #005a9e);
            box-shadow: 0 8px 18px rgba(0,120,212,0.25);
        }

        .demo-note {
            background: #f1f5f9;
            border-radius: 18px;
            padding: 12px 16px;
            margin-top: 20px;
            font-size: 0.75rem;
            color: #334155;
            text-align: center;
            border: 1px solid #e2e8f0;
        }

        .inline-link {
            color: #0078d4;
            text-decoration: none;
            font-weight: 600;
        }

        hr {
            margin: 16px 0;
            border: none;
            border-top: 1px solid #eef2ff;
        }

        /* registration specific adjustments */
        textarea {
            resize: vertical;
            min-height: 70px;
        }

        .flex-row {
            display: flex;
            gap: 12px;
        }
        .flex-row .field-group {
            flex: 1;
        }

        @media (max-width: 480px) {
            .form-pane {
                padding: 1.5rem;
            }
            .flex-row {
                flex-direction: column;
                gap: 0;
            }
        }

        .success-banner {
            background: #e6f7e6;
            border-radius: 16px;
            padding: 12px;
            text-align: center;
            margin-bottom: 1rem;
            color: #2e7d32;
            font-weight: 500;
            font-size: 0.85rem;
            border-left: 4px solid #22c55e;
        }
    </style>
</head>
<body>

<div class="auth-container" id="authRoot">
    <!-- Tabs header -->
    <div class="auth-header">
        <button class="tab-btn active" id="loginTabBtn">🔐 Sign in</button>
        <button class="tab-btn" id="registerTabBtn">📝 Create account</button>
    </div>

    <!-- LOGIN PANE -->
    <div id="loginPane" class="form-pane active-pane">
        <h2>Azure DevOps</h2>
        <form id="loginForm" onsubmit="return handleLoginSubmit(event)">
            <div class="field-group">
                <label>📧 Email or Username</label>
                <input type="email" id="loginEmail" placeholder="you@example.com or registered email" autocomplete="email">
                <div id="loginEmailMsg" class="error" style="display: none;"></div>
            </div>
            <div class="field-group">
                <label>🔒 Password</label>
                <input type="password" id="loginPassword" placeholder="••••••••" autocomplete="current-password">
                <div id="loginPassMsg" class="error" style="display: none;"></div>
            </div>
            <button type="submit">Login to workspace →</button>
            <div class="demo-note">
                💡 <strong>Demo credentials</strong><br>
                Email: <span class="inline-link">dev@azure.com</span> / Password: <span class="inline-link">dev123</span><br>
                Or use any registered account (via Register tab)
            </div>
        </form>
    </div>

    <!-- REGISTRATION PANE (enhanced from original, with same robust validation) -->
    <div id="registerPane" class="form-pane">
        <h2>DevOps Registration</h2>
        <form id="registerForm" onsubmit="return validateRegistrationForm(event)">
            <div class="flex-row">
                <div class="field-group">
                    <label>First Name</label>
                    <input type="text" id="regFname" placeholder="Alex" autocomplete="given-name">
                    <div id="regFnameMsg"></div>
                </div>
                <div class="field-group">
                    <label>Last Name</label>
                    <input type="text" id="regLname" placeholder="Rivera" autocomplete="family-name">
                    <div id="regLnameMsg"></div>
                </div>
            </div>
            <div class="field-group">
                <label>🔐 Password</label>
                <input type="password" id="regPassword" placeholder="Min 6 characters" autocomplete="new-password">
                <div id="regPassMsg"></div>
            </div>
            <div class="field-group">
                <label>📧 Email (will be login ID)</label>
                <input type="email" id="regEmail" placeholder="alex@devops.com" autocomplete="email">
                <div id="regEmailMsg"></div>
            </div>
            <div class="field-group">
                <label>📱 Mobile Number</label>
                <input type="tel" id="regMobile" placeholder="9876543210" autocomplete="tel">
                <div id="regMobileMsg"></div>
            </div>
            <div class="field-group">
                <label>🏠 Address</label>
                <textarea id="regAddress" placeholder="Street, city, zip code" rows="2"></textarea>
                <div id="regAddrMsg"></div>
            </div>
            <button type="submit">🚀 Register & Login</button>
            <div class="demo-note">
                ✅ <strong>Validation rules</strong> : First name (min 6 letters, alphabets), Last name required, Password ≥6 chars, valid email, 10-digit mobile, address required.
            </div>
        </form>
    </div>
</div>

<script>
    // ---------- STORAGE KEYS (simulated user database) ----------
    const USERS_STORAGE_KEY = "azure_devops_users";

    // Load existing users from localStorage or initialize empty array
    function getRegisteredUsers() {
        const stored = localStorage.getItem(USERS_STORAGE_KEY);
        if (stored) {
            try {
                return JSON.parse(stored);
            } catch(e) { return []; }
        }
        // Preload demo user for convenience (so login with dev@azure.com / dev123 works)
        const defaultUsers = [
            {
                firstName: "Demo",
                lastName: "Engineer",
                email: "dev@azure.com",
                password: "dev123",
                mobile: "9999999999",
                address: "Redmond, WA"
            }
        ];
        localStorage.setItem(USERS_STORAGE_KEY, JSON.stringify(defaultUsers));
        return defaultUsers;
    }

    function saveUser(userObj) {
        const users = getRegisteredUsers();
        // avoid duplicate emails
        const exists = users.some(u => u.email.toLowerCase() === userObj.email.toLowerCase());
        if (exists) return false;
        users.push(userObj);
        localStorage.setItem(USERS_STORAGE_KEY, JSON.stringify(users));
        return true;
    }

    function findUserByEmailAndPassword(email, password) {
        const users = getRegisteredUsers();
        return users.find(u => u.email.toLowerCase() === email.toLowerCase() && u.password === password);
    }

    // ---------------- REGISTRATION VALIDATION (enhanced) ----------------
    const regFname = document.getElementById('regFname');
    const regLname = document.getElementById('regLname');
    const regPassword = document.getElementById('regPassword');
    const regEmail = document.getElementById('regEmail');
    const regMobile = document.getElementById('regMobile');
    const regAddress = document.getElementById('regAddress');

    const regFnameMsg = document.getElementById('regFnameMsg');
    const regLnameMsg = document.getElementById('regLnameMsg');
    const regPassMsg = document.getElementById('regPassMsg');
    const regEmailMsg = document.getElementById('regEmailMsg');
    const regMobileMsg = document.getElementById('regMobileMsg');
    const regAddrMsg = document.getElementById('regAddrMsg');

    function setValid(field, msgEl, text) {
        field.classList.add("valid");
        field.classList.remove("invalid");
        msgEl.className = "successText";
        msgEl.innerHTML = "✔ " + text;
    }

    function setInvalid(field, msgEl, text) {
        field.classList.add("invalid");
        field.classList.remove("valid");
        msgEl.className = "error";
        msgEl.innerHTML = "✖ " + text;
    }

    function validateRegFirstName() {
        let val = regFname.value.trim();
        let pattern = /^[A-Za-z]+$/;
        if (val.length >= 6 && pattern.test(val)) {
            setValid(regFname, regFnameMsg, "Looks good");
            return true;
        } else {
            setInvalid(regFname, regFnameMsg, "Min 6 letters, alphabets only");
            return false;
        }
    }

    function validateRegLastName() {
        let val = regLname.value.trim();
        if (val !== "") {
            setValid(regLname, regLnameMsg, "OK");
            return true;
        } else {
            setInvalid(regLname, regLnameMsg, "Last name required");
            return false;
        }
    }

    function validateRegPassword() {
        let pwd = regPassword.value;
        if (pwd.length >= 6) {
            setValid(regPassword, regPassMsg, "Strong enough");
            return true;
        } else {
            setInvalid(regPassword, regPassMsg, "Minimum 6 characters");
            return false;
        }
    }

    function validateRegEmail() {
        let emailVal = regEmail.value.trim();
        let pattern = /^[^\s@]+@([^\s@]+\.)+[a-zA-Z]{2,}$/;  // robust email pattern
        // additional: check if email already registered
        if (pattern.test(emailVal)) {
            // check uniqueness (optional but improves UX)
            const users = getRegisteredUsers();
            const isDuplicate = users.some(u => u.email.toLowerCase() === emailVal.toLowerCase());
            if (isDuplicate) {
                setInvalid(regEmail, regEmailMsg, "Email already registered! Try login.");
                return false;
            } else {
                setValid(regEmail, regEmailMsg, "Valid email & available");
                return true;
            }
        } else {
            setInvalid(regEmail, regEmailMsg, "Invalid email format (e.g., name@domain.com)");
            return false;
        }
    }

    function validateRegMobile() {
        let mob = regMobile.value.trim();
        let pattern = /^[0-9]{10}$/;
        if (pattern.test(mob)) {
            setValid(regMobile, regMobileMsg, "Valid number");
            return true;
        } else {
            setInvalid(regMobile, regMobileMsg, "Enter 10 digits");
            return false;
        }
    }

    function validateRegAddress() {
        let addr = regAddress.value.trim();
        if (addr !== "") {
            setValid(regAddress, regAddrMsg, "OK");
            return true;
        } else {
            setInvalid(regAddress, regAddrMsg, "Address required");
            return false;
        }
    }

    // Attach event listeners for dynamic registration validation
    if (regFname) regFname.addEventListener('keyup', validateRegFirstName);
    if (regLname) regLname.addEventListener('keyup', validateRegLastName);
    if (regPassword) regPassword.addEventListener('keyup', validateRegPassword);
    if (regEmail) regEmail.addEventListener('keyup', validateRegEmail);
    if (regMobile) regMobile.addEventListener('keyup', validateRegMobile);
    if (regAddress) regAddress.addEventListener('keyup', validateRegAddress);

    // Final registration handler
    function validateRegistrationForm(event) {
        event.preventDefault();
        const isFnameValid = validateRegFirstName();
        const isLnameValid = validateRegLastName();
        const isPwdValid = validateRegPassword();
        const isEmailValid = validateRegEmail();
        const isMobileValid = validateRegMobile();
        const isAddrValid = validateRegAddress();

        if (isFnameValid && isLnameValid && isPwdValid && isEmailValid && isMobileValid && isAddrValid) {
            // Create new user object
            const newUser = {
                firstName: regFname.value.trim(),
                lastName: regLname.value.trim(),
                email: regEmail.value.trim().toLowerCase(),
                password: regPassword.value,
                mobile: regMobile.value.trim(),
                address: regAddress.value.trim()
            };
            const saveSuccess = saveUser(newUser);
            if (saveSuccess) {
                alert("🎉 Registration Successful! You can now login with your credentials.");
                // Optional: redirect to login pane and pre-fill email
                document.getElementById("loginTabBtn").click();
                const loginEmailField = document.getElementById("loginEmail");
                if (loginEmailField) loginEmailField.value = newUser.email;
                // Clear registration form for next use
                document.getElementById("registerForm").reset();
                // reset validation styles
                [regFname, regLname, regPassword, regEmail, regMobile, regAddress].forEach(field => {
                    if(field) {
                        field.classList.remove("valid", "invalid");
                    }
                });
                [regFnameMsg, regLnameMsg, regPassMsg, regEmailMsg, regMobileMsg, regAddrMsg].forEach(msg => {
                    if(msg) msg.innerHTML = "";
                });
            } else {
                alert("⚠️ Email already exists. Please use a different email or go to Login.");
                validateRegEmail(); // re-check to show duplicate message
            }
        } else {
            alert("⚠ Please fix errors before submitting registration.");
        }
        return false;
    }

    // ------------------- LOGIN HANDLER -------------------
    function handleLoginSubmit(event) {
        event.preventDefault();
        const loginEmail = document.getElementById('loginEmail').value.trim();
        const loginPassword = document.getElementById('loginPassword').value;
        const emailMsgDiv = document.getElementById('loginEmailMsg');
        const passMsgDiv = document.getElementById('loginPassMsg');

        let isValid = true;
        if (!loginEmail) {
            emailMsgDiv.style.display = "block";
            emailMsgDiv.innerHTML = "✖ Email is required";
            isValid = false;
        } else if (!loginEmail.includes("@") || !/^[^\s@]+@([^\s@]+\.)+[a-zA-Z]{2,}$/.test(loginEmail)) {
            emailMsgDiv.style.display = "block";
            emailMsgDiv.innerHTML = "✖ Please enter a valid email address";
            isValid = false;
        } else {
            emailMsgDiv.style.display = "none";
        }

        if (!loginPassword) {
            passMsgDiv.style.display = "block";
            passMsgDiv.innerHTML = "✖ Password required";
            isValid = false;
        } else if (loginPassword.length < 1) {
            passMsgDiv.style.display = "block";
            passMsgDiv.innerHTML = "✖ Invalid password";
            isValid = false;
        } else {
            passMsgDiv.style.display = "none";
        }

        if (isValid) {
            const user = findUserByEmailAndPassword(loginEmail, loginPassword);
            if (user) {
                // Success: display welcome overlay and reset
                alert(`✅ Welcome back, ${user.firstName} ${user.lastName}!\nYou have successfully logged into Azure DevOps Portal.`);
                // optional: simulate redirect or clear form
                document.getElementById('loginForm').reset();
                emailMsgDiv.style.display = "none";
                passMsgDiv.style.display = "none";
                // You can also add a small visual effect
            } else {
                passMsgDiv.style.display = "block";
                passMsgDiv.innerHTML = "✖ Incorrect email or password. Please try again or register.";
                emailMsgDiv.style.display = "none";
            }
        }
        return false;
    }

    // ---------------- TAB TOGGLE LOGIC (Login / Register) ----------------
    const loginTabBtn = document.getElementById('loginTabBtn');
    const registerTabBtn = document.getElementById('registerTabBtn');
    const loginPane = document.getElementById('loginPane');
    const registerPane = document.getElementById('registerPane');

    function setActiveTab(active) {
        if (active === 'login') {
            loginTabBtn.classList.add('active');
            registerTabBtn.classList.remove('active');
            loginPane.classList.add('active-pane');
            registerPane.classList.remove('active-pane');
            // optional clear any login errors on switch
        } else {
            registerTabBtn.classList.add('active');
            loginTabBtn.classList.remove('active');
            registerPane.classList.add('active-pane');
            loginPane.classList.remove('active-pane');
            // trigger fresh validation for registration optional
        }
    }

    loginTabBtn.addEventListener('click', () => setActiveTab('login'));
    registerTabBtn.addEventListener('click', () => setActiveTab('register'));

    // Prefill demo login hint: show demo credentials easily
    const demoFill = () => {
        const loginEmailField = document.getElementById('loginEmail');
        const loginPassField = document.getElementById('loginPassword');
        if(loginEmailField && loginEmailField.value === "") {
            // optional but not intrusive: we let user click demo note.
        }
    };
    // Add small helper to fill demo when clicking demo note text? Or just provide visual.
    // To improve UX, attach custom click on demo-note for quick fill
    const demoNoteDiv = document.querySelector('.demo-note');
    if (demoNoteDiv && loginPane) {
        // but avoid double attachment; add quick listener for demofill.
        const demoTextSpan = demoNoteDiv.querySelectorAll('.inline-link');
        if(demoTextSpan.length >= 2) {
            demoNoteDiv.style.cursor = "pointer";
            demoNoteDiv.addEventListener('click', (e) => {
                if(loginPane.classList.contains('active-pane')) {
                    document.getElementById('loginEmail').value = "dev@azure.com";
                    document.getElementById('loginPassword').value = "dev123";
                    const emailMsg = document.getElementById('loginEmailMsg');
                    const passMsg = document.getElementById('loginPassMsg');
                    if(emailMsg) emailMsg.style.display = "none";
                    if(passMsg) passMsg.style.display = "none";
                } else {
                    // optional fill registration example
                    if(registerPane.classList.contains('active-pane')) {
                        if(regEmail && !regEmail.value) regEmail.value = "newuser@devops.com";
                        if(regPassword && !regPassword.value) regPassword.value = "secure123";
                        if(regFname && !regFname.value) regFname.value = "AzureDev";
                        if(regLname && !regLname.value) regLname.value = "Ops";
                        if(regMobile && !regMobile.value) regMobile.value = "9988776655";
                        if(regAddress && !regAddress.value) regAddress.value = "Cloud City, DevOps Lane";
                        // trigger validation to make UI clear
                        validateRegFirstName(); validateRegLastName(); validateRegPassword();
                        validateRegEmail(); validateRegMobile(); validateRegAddress();
                    }
                }
            });
        }
    }

    // For cleaner UX: live validation on blur for login (not mandatory but nice)
    const loginEmailInput = document.getElementById('loginEmail');
    const loginPassInput = document.getElementById('loginPassword');
    if(loginEmailInput) {
        loginEmailInput.addEventListener('input', () => {
            const msg = document.getElementById('loginEmailMsg');
            if(msg) msg.style.display = "none";
        });
        loginPassInput.addEventListener('input', () => {
            const msg = document.getElementById('loginPassMsg');
            if(msg) msg.style.display = "none";
        });
    }
    // Ensure localStorage demo user preload is consistent
    (function initDemoUserConsistency() {
        let users = getRegisteredUsers();
        const demoExists = users.some(u => u.email === "dev@azure.com");
        if(!demoExists) {
            users.push({
                firstName: "Demo",
                lastName: "Engineer",
                email: "dev@azure.com",
                password: "dev123",
                mobile: "9999999999",
                address: "Redmond, WA"
            });
            localStorage.setItem(USERS_STORAGE_KEY, JSON.stringify(users));
        }
    })();
</script>
</body>
</html>
