<script>
    let username = "";
    let password = "";
</script>

<div class="login-container">
    <div class="login-card">
        <h2 class="animated-title">Login</h2>
        <form>
            <div class="input-group">
                <label for="username">Username</label>
                <input type="text" id="username" bind:value={username} />
            </div>
            <div class="input-group">
                <label for="password">Password</label>
                <input type="password" id="password" bind:value={password} />
            </div>
            <button type="submit">Login</button>
        </form>
        <p>
            New User? <a href="/register">Register</a>
        </p>
        <p>
            <a href="/todo">Go to To-Do List</a>
        </p>
    </div>
</div>

<style>
    @import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap");

    .login-container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        background: url("path/to/your/background-image.jpg") no-repeat center
            center fixed;
        background-size: cover;
    }

    .login-card {
        background: rgba(255, 255, 255, 0.9);
        padding: 2rem;
        border-radius: 12px;
        box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
        width: 90%;
        max-width: 300px;
        text-align: center;
        font-family: "Roboto", sans-serif;
        transition:
            transform 0.3s ease,
            box-shadow 0.3s ease,
            background 0.3s ease;
    }

    .login-card:hover {
        transform: translateY(-10px);
        box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
    }

    .login-card h2 {
        margin-bottom: 1.5rem;
        font-size: 1.8rem;
        background: linear-gradient(45deg, #ff007f, #7f00ff, #00c9ff);
        -webkit-background-clip: text;
        -webkit-text-fill-color: transparent;
        background-clip: text;
        color: transparent;
        animation: colorChange 5s ease-in-out infinite;
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

    .input-group {
        margin-bottom: 1.5rem;
        text-align: left;
    }

    .input-group label {
        display: block;
        margin-bottom: 0.5rem;
        color: #666;
        font-size: 1rem;
    }

    .input-group input {
        width: 100%;
        padding: 0.75rem;
        border: 1px solid #ccc;
        border-radius: 4px;
        font-size: 1rem;
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
        background: linear-gradient(135deg, #007bff, #0056b3);
        color: white;
        font-size: 1.1rem;
        font-weight: 500;
        cursor: pointer;
        transition:
            background 0.3s ease,
            transform 0.3s ease,
            box-shadow 0.3s ease;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    button:hover {
        background: linear-gradient(135deg, #0056b3, #003f7f);
        transform: translateY(-2px);
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3);
    }

    button:active {
        transform: translateY(1px);
        box-shadow: 0 2px 6px rgba(0, 0, 0, 0.2);
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
