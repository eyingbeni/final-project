<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Fitness Tracker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f4f6f8;
            margin: 0;
        }

        /* APP HEADER / LOGO */
        .app-header {
            background: #343a40;
            color: white;
            padding: 20px;
            text-align: center;
        }

        /* NAV BAR */
        nav {
            background: #2c7be5;
            padding: 12px;
            display: flex;
            justify-content: center;
            gap: 30px;
        }
        nav button {
            background: white;
            color: #2c7be5;
            border: none;
            padding: 10px 22px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            width: auto;
        }
        nav button:hover {
            background: #e6ecff;
        }

        /* PAGE CONTAINER */
        .container {
            max-width: 700px;
            margin: 30px auto;
            background: white;
            padding: 20px;
            border-radius: 10px;
        }

        /* FORM INPUTS */
        input {
            width: 100%;
            padding: 10px;
            margin: 8px 0;
            font-size: 16px;
        }

        /* FORM BUTTON */
        .form-btn {
            width: 100%;
            padding: 10px;
            background: #2c7be5;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin-top: 10px;
        }

        /* WORKOUT ITEMS */
        .workout {
            border-left: 5px solid #2c7be5;
            padding: 10px;
            margin-bottom: 10px;
        }

        /* MOTIVATION IMAGES */
        .images {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            justify-content: center;
            margin-bottom: 20px;
        }
        .images img {
            width: 200px;
            border-radius: 10px;
        }

        /* PAGE SWITCHING */
        .page {
            display: none;
        }
        .active {
            display: block;
        }
    </style>
</head>
<body>

<!-- LOGO -->
<div class="app-header">
    <h1>🏋️ Fitness Tracker</h1>
</div>

<!-- NAV BAR -->
<nav>
    <button type="button" onclick="showPage('addPage')">➕ Add Workout</button>
    <button type="button" onclick="showPage('logPage')">📋 Workout Log</button>
</nav>

<!-- ADD WORKOUT PAGE -->
<div id="addPage" class="page active">
    <div class="container">
        <h2>Add Workout</h2>
        <input type="text" id="activity" placeholder="Activity (e.g., Ran 5km)">
        <input type="date" id="date">
        <input type="number" id="duration" placeholder="Duration (minutes)">
        <button class="form-btn" onclick="addWorkout()">Add Workout</button>
    </div>
</div>

<!-- WORKOUT LOG PAGE -->
<div id="logPage" class="page">
    <div class="container">
        <h2>Workout Log</h2>

        <!-- MOTIVATION IMAGES -->
        <div class="images">
            <img src="https://images.unsplash.com/photo-1571019613454-1cb2f99b2d8b?auto=format&fit=crop&w=400&q=80" alt="Running">
            <img src="https://images.unsplash.com/photo-1517836357463-d25dfeac3438?auto=format&fit=crop&w=400&q=80" alt="Weight Lifting">
              <img src="img.avif">      
        
        </div>

        <!-- WORKOUT LIST -->
        <div id="workoutList"></div>
    </div>
</div>

<script>
function showPage(pageId) {
    document.querySelectorAll(".page").forEach(page => {
        page.classList.remove("active");
    });
    document.getElementById(pageId).classList.add("active");

    if (pageId === "logPage") {
        renderWorkouts();
    }
}

function addWorkout() {
    const activity = document.getElementById("activity").value;
    const date = document.getElementById("date").value;
    const duration = document.getElementById("duration").value;

    if (!activity || !date || !duration) {
        alert("Please fill all fields!");
        return;
    }

    let workouts = JSON.parse(localStorage.getItem("workouts")) || [];
    workouts.push({ activity, date, duration });
    localStorage.setItem("workouts", JSON.stringify(workouts));

    alert("Workout added!");

    document.getElementById("activity").value = "";
    document.getElementById("date").value = "";
    document.getElementById("duration").value = "";

    showPage("logPage"); // switch to log page automatically
}

function renderWorkouts() {
    const workoutList = document.getElementById("workoutList");
    const workouts = JSON.parse(localStorage.getItem("workouts")) || [];

    workoutList.innerHTML = "";

    if (workouts.length === 0) {
        workoutList.innerHTML = "<p>No workouts logged yet.</p>";
        return;
    }

    workouts.forEach(workout => {
        const div = document.createElement("div");
        div.className = "workout";
        div.innerHTML = `
            <strong>${workout.activity}</strong><br>
            Date: ${workout.date}<br>
            Duration: ${workout.duration} minutes
        `;
        workoutList.appendChild(div);
    });
}
</script>

</body>
</html>
