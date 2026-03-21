# 
Calvin
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mzzkznb | Roblox Profile</title>

<style>
    body {
        margin: 0;
        font-family: Arial, sans-serif;
        background: linear-gradient(135deg, #0f0f0f, #1a1a2e);
        color: white;
    }

    header {
        text-align: center;
        padding: 40px;
        background: #111;
        border-bottom: 2px solid #00ffcc;
    }

    header h1 {
        font-size: 40px;
        color: #00ffcc;
    }

    section {
        padding: 30px;
        max-width: 900px;
        margin: auto;
    }

    .card {
        background: #1f1f2e;
        padding: 20px;
        margin: 20px 0;
        border-radius: 12px;
        box-shadow: 0 0 15px #00ffcc33;
    }

    h2 {
        color: #00ffcc;
    }

    .stats {
        display: flex;
        justify-content: space-around;
        text-align: center;
        flex-wrap: wrap;
    }

    .stat {
        font-size: 18px;
        margin: 10px;
    }

    .btn {
        display: inline-block;
        padding: 10px 20px;
        margin: 10px;
        background: #00ffcc;
        color: black;
        text-decoration: none;
        border-radius: 8px;
        font-weight: bold;
    }

    .avatar {
        display: block;
        margin: 20px auto;
        border-radius: 50%;
        box-shadow: 0 0 20px #00ffcc;
    }

</style>
</head>

<body>

<header>
    <h1>🎮 Mzzkznb</h1>
    <p>Roblox Rivals Player | Live Profile</p>
    <img id="avatar" class="avatar" width="150">
</header>

<section>

    <div class="card">
        <h2>👤 Live Roblox Info</h2>
        <div class="stats">
            <div class="stat">Username: <strong id="name">Loading...</strong></div>
            <div class="stat">User ID: <strong id="userid">Loading...</strong></div>
            <div class="stat">Account Age: <strong id="age">Loading...</strong></div>
        </div>
    </div>

    <div class="card">
        <h2>🌐 Profile</h2>
        <a href="https://www.roblox.com/users/profile?username=Mzzkznb" target="_blank" class="btn">
            View Roblox Profile
        </a>
    </div>

</section>

<script>
const username = "Mzzkznb";

// STEP 1: Get User ID
fetch("https://users.roblox.com/v1/usernames/users", {
    method: "POST",
    headers: {"Content-Type": "application/json"},
    body: JSON.stringify({usernames: [username]})
})
.then(res => res.json())
.then(data => {
    const user = data.data[0];
    document.getElementById("name").textContent = user.name;
    document.getElementById("userid").textContent = user.id;

    // STEP 2: Get Avatar
    fetch(`https://thumbnails.roblox.com/v1/users/avatar?userIds=${user.id}&size=150x150&format=Png`)
    .then(res => res.json())
    .then(img => {
        document.getElementById("avatar").src = img.data[0].imageUrl;
    });

    // STEP 3: Get Account Age
    fetch(`https://users.roblox.com/v1/users/${user.id}`)
    .then(res => res.json())
    .then(info => {
        const created = new Date(info.created);
        const now = new Date();
        const ageDays = Math.floor((now - created) / (1000 * 60 * 60 * 24));
        document.getElementById("age").textContent = ageDays + " days";
    });
});
</script>

</body>
</html>