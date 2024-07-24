<script>
    let firstName = "";
    let lastName = "";
    let email = "";
    let password = "";
    let confirmPassword = "";
</script>

<div class="register-container">
    <div class="register-card">
        <h2 class="animated-title">Register</h2>
        <form>
            <div class="name-group">
                <div class="input-group">
                    <label for="firstName">First Name</label>
                    <input type="text" id="firstName" bind:value={firstName} />
                </div>
                <div class="input-group">
                    <label for="lastName">Last Name</label>
                    <input type="text" id="lastName" bind:value={lastName} />
                </div>
            </div>
            <div class="input-group">
                <label for="email">Email</label>
                <input type="email" id="email" bind:value={email} />
            </div>
            <div class="input-group">
                <label for="password">Password</label>
                <input type="password" id="password" bind:value={password} />
            </div>
            <div class="input-group">
                <label for="confirmPassword">Confirm Password</label>
                <input
                    type="password"
                    id="confirmPassword"
                    bind:value={confirmPassword}
                />
            </div>
            <button type="submit">Register</button>
        </form>
        <p>
            Already registered? <a href="/">Login</a>
        </p>
    </div>
</div>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap");

    .register-container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background: url("path/to/your/background-image.jpg") no-repeat center
            center fixed;
        background-size: cover;
    }

    .register-card {
        background: rgba(255, 255, 255, 0.9);
        padding: 2rem;
        border-radius: 12px;
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
        width: 90%;
        max-width: 360px;
        text-align: center;
        font-family: "Roboto", sans-serif;
        transition:
            transform 0.3s ease,
            box-shadow 0.3s ease,
            background 0.3s ease;
    }

    .register-card:hover {
        transform: translateY(-10px);
        box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    }

    .animated-title {
        margin-bottom: 1.5rem;
        font-size: 2rem;
        background: linear-gradient(45deg, #ff007f, #7f00ff, #00c9ff);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        color: transparent;
        animation: colorChange 4s linear infinite;
    }

    @keyframes colorChange {
        0% {
            background-position: 0% 0%;
        }
        50% {
            background-position: 100% 100%;
        }
        100% {
            background-position: 0% 0%;
        }
    }

    .name-group {
        display: flex;
        justify-content: space-between;
        gap: 1rem;
    }

    .input-group {
        margin-bottom: 1.5rem;
        text-align: left;
        flex: 1;
    }

    .input-group label {
        display: block;
        margin-bottom: 0.5rem;
        color: #666;
        font-size: 0.9rem;
    }

    .input-group input {
        width: 100%;
        padding: 0.75rem;
        border: 1px solid #ccc;
        border-radius: 4px;
        font-size: 0.9rem;
        transition:
            border-color 0.3s ease,
            box-shadow 0.3s ease;
    }

    .input-group input:focus {
        border-color: #007bff;
        box-shadow: 0 0 8px rgba(0, 123, 255, 0.3);
        outline: none;
    }

    button {
        width: 100%;
        padding: 0.75rem;
        border: none;
        border-radius: 8px;
        background: linear-gradient(135deg, #ff0099, #493240);
        color: white;
        font-size: 1.1rem;
        font-weight: 500;
        cursor: pointer;
        transition:
            background 0.3s ease,
            transform 0.3s ease,
            box-shadow 0.3s ease;
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
    }

    button:hover {
        background: linear-gradient(135deg, #493240, #ff0099);
        transform: translateY(-2px);
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
    }

    button:active {
        transform: translateY(1px);
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    p {
        margin-top: 1.5rem;
        color: #666;
    }

    a {
        color: #007bff;
        text-decoration: none;
        font-weight: 500;
        transition:
            color 0.3s ease,
            text-shadow 0.3s ease;
    }

    a:hover {
        color: #0056b3;
        text-decoration: underline;
        text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
    }
</style>
