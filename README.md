<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>HHOD Calorie Calculator</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link href="https://fonts.googleapis.com/css2?family=League+Spartan:wght@400;500;700&display=swap" rel="stylesheet">
  <style>
    * { box-sizing: border-box; }
    body {
      font-family: 'League Spartan', sans-serif;
      margin: 0;
      padding: 0;
      background: #fff3eb;
      color: #333;
    }
    .container {
      max-width: 480px;
      width: 95%;
      margin: 20px auto;
      background: white;
      border-top: 6px solid #f37221;
      border-radius: 10px;
      padding: 20px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.08);
    }
    h2 {
      text-align: center;
      color: #f37221;
      margin-bottom: 20px;
      font-size: 22px;
    }
    label {
      display: block;
      margin-top: 15px;
      font-weight: bold;
      color: #f37221;
      font-size: 14px;
    }
    input, select {
      width: 100%;
      padding: 10px;
      margin-top: 6px;
      border-radius: 6px;
      border: 1px solid #ccc;
      font-family: 'League Spartan', sans-serif;
      font-size: 14px;
    }
    .unit-tabs {
      display: flex;
      margin: 15px 0;
    }
    .unit-tabs button {
      flex: 1;
      padding: 10px;
      background: #eee;
      border: none;
      cursor: pointer;
      font-weight: bold;
    }
    .unit-tabs button.active {
      background: #f37221;
      color: white;
    }
    .unit-section {
      display: none;
    }
    .unit-section.active {
      display: block;
    }
    button.submit, .email-button {
      margin-top: 25px;
      width: 100%;
      padding: 12px;
      font-size: 16px;
      background-color: #f37221;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    .results {
      margin-top: 25px;
      background: #f7f7f7;
      padding: 15px;
      border-top: 6px solid #f37221;
      border-radius: 8px;
      font-size: 14px;
      text-align: center;
    }
    footer {
      display: flex;
      justify-content: center;
      align-items: center;
      flex-wrap: wrap;
      gap: 20px;
      text-align: center;
      margin-top: 40px;
      padding: 20px;
      background: #f37221;
      color: white;
      font-size: 14px;
    }
    footer a {
      color: white;
      text-decoration: none;
      font-weight: bold;
    }
    .footer-icon {
      width: 18px;
      vertical-align: middle;
      margin-right: 6px;
    }
    .popup-overlay {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.6);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }
    .popup {
      background: white;
      padding: 25px;
      border-radius: 8px;
      width: 90%;
      max-width: 400px;
      box-shadow: 0 0 20px rgba(0,0,0,0.2);
    }
    .popup h3 {
      margin-top: 0;
      color: #f37221;
      text-align: center;
    }
    .popup label {
      margin-top: 10px;
      display: block;
    }
    .popup button {
      margin-top: 15px;
      background-color: #f37221;
      color: white;
      border: none;
      padding: 10px;
      width: 100%;
      border-radius: 6px;
      cursor: pointer;
    }
  </style>
</head>
<body>

<div class="container">
  <h2>HHOD Calorie Calculator</h2>

  <form id="calorieForm">
    <div class="unit-tabs">
      <button type="button" id="metricBtn" class="active" onclick="switchToMetric()">Metric</button>
      <button type="button" id="imperialBtn" onclick="switchToImperial()">Imperial</button>
    </div>

    <label for="gender">Gender at birth</label>
    <select id="gender" required>
      <option value="" disabled selected>Select gender</option>
      <option value="male">Male</option>
      <option value="female">Female</option>
    </select>

    <label for="age">Age</label>
    <input type="number" id="age" required placeholder="e.g. 30" />

    <div id="metricSection" class="unit-section active">
      <label for="height">Height (cm)</label>
      <input type="number" id="height" step="0.1" placeholder="e.g. 175.5" />

      <label for="weight">Weight (kg)</label>
      <input type="number" id="weight" step="0.1" placeholder="e.g. 70.5" />
    </div>

    <div id="imperialSection" class="unit-section">
      <label for="heightFeet">Height</label>
      <div style="display: flex; gap: 10px;">
        <input type="number" id="heightFeet" step="1" placeholder="Feet" style="flex: 1;" />
        <input type="number" id="heightInches" step="0.1" placeholder="Inches" style="flex: 1;" />
      </div>

      <label for="weightStone">Weight</label>
      <div style="display: flex; gap: 10px;">
        <input type="number" id="weightStone" step="1" placeholder="Stone" style="flex: 1;" />
        <input type="number" id="weightPounds" step="0.1" placeholder="Pounds" style="flex: 1;" />
      </div>
    </div>

    <label for="activity">Activity</label>
    <select id="activity" required>
      <option value="" disabled selected>Choose activity level</option>
      <option value="1.2">Sedentary (little or no exercise)</option>
      <option value="1.375">Lightly active (1–3 days/week)</option>
      <option value="1.55">Moderately active (3–5 days/week)</option>
      <option value="1.725">Very active (6–7 days/week)</option>
      <option value="1.9">Extra active (hard training/physical job)</option>
    </select>

    <label for="goal">Goal</label>
    <select id="goal" required>
      <option value="" disabled selected>Choose goal</option>
      <option value="maintain">Maintain weight & body composition</option>
      <option value="lose">Lose weight</option>
      <option value="gain">Gain weight & muscle</option>
    </select>

    <label for="macroSplit">Macro Split (Protein/Carbohydrates/Fats)</label>
    <select id="macroSplit" required>
      <option value="" disabled selected>Choose macro split</option>
      <option value="normal">Normal</option>
      <option value="highProtein">High protein / low carb</option>
      <option value="keto">Keto</option>
      <option value="vegan">Vegan</option>
      <option value="paleo">Paleo</option>
    </select>

    <button type="submit" class="submit">Generate Calories & Macros</button>
  </form>

  <div id="results" class="results" style="display: none;"></div>
  <div id="disclaimer" class="results" style="display: none; margin-top: 15px; font-size: 13px; color: #666;">
    <p><strong>Please Note:</strong> If you are on medication or have health conditions, these results may not be accurate and would be best to speak to a personal trainer in more detail to help you with your goal.</p>
  </div>
  <button id="emailPrompt" class="email-button" style="display:none;" onclick="showPopup()">Would you like your results sent to you?</button>
</div>

<!-- Popup -->
<div class="popup-overlay" id="popupOverlay" onclick="closePopup(event)">
  <form action="https://formspree.io/f/xeokbqge" method="POST" class="popup" onclick="event.stopPropagation()">
    <h3>Email Your Results</h3>
    <p style="text-align: center; margin-bottom: 15px; color: #666;">A personal trainer from Health Hub On Demand will send your results via email or WhatsApp.</p>
    <label for="name">Name</label>
    <input type="text" name="name" required />

    <label for="email">Email</label>
    <input type="email" name="email" required />

    <label for="phone">Phone Number</label>
    <input type="tel" name="phone" required />

    <label style="text-align: center;">
      <input type="checkbox" name="trainer_interest" value="Yes" />
      Would you like the Personal Trainer to discuss your Exercise and Nutrition goals with you?
    </label>

    <button type="submit">Send Results</button>
    <button type="button" onclick="closePopup()">Close</button>
  </form>
</div>

<footer>
  <a href="https://www.instagram.com/heathhubod/" target="_blank">
    <img class="footer-icon" src="https://upload.wikimedia.org/wikipedia/commons/a/a5/Instagram_icon.png" alt="Instagram" />
    @heathhubod
  </a>
  <a href="https://www.thehealthhubgroup.com/hhod" target="_blank">www.thehealthhubgroup.com/hhod</a>
</footer>

<script>
  function showPopup() {
    document.getElementById("popupOverlay").style.display = "flex";
  }
  
  function closePopup(event) {
    if (event) event.preventDefault();
    document.getElementById("popupOverlay").style.display = "none";
  }

  function switchToMetric() {
    document.getElementById("metricBtn").classList.add("active");
    document.getElementById("imperialBtn").classList.remove("active");
    document.getElementById("metricSection").classList.add("active");
    document.getElementById("imperialSection").classList.remove("active");
    
    // Convert imperial values to metric if they exist
    const feet = parseFloat(document.getElementById("heightFeet").value) || 0;
    const inches = parseFloat(document.getElementById("heightInches").value) || 0;
    const stone = parseFloat(document.getElementById("weightStone").value) || 0;
    const pounds = parseFloat(document.getElementById("weightPounds").value) || 0;
    
    if (feet > 0 || inches > 0) {
      const heightCm = (feet * 12 + inches) * 2.54;
      document.getElementById("height").value = (Math.round(heightCm * 10) / 10).toFixed(1);
    }
    
    if (stone > 0 || pounds > 0) {
      const totalPounds = stone * 14 + pounds;
      const weightKg = totalPounds * 0.453592;
      document.getElementById("weight").value = (Math.round(weightKg * 10) / 10).toFixed(1);
    }
  }

  function switchToImperial() {
    document.getElementById("metricBtn").classList.remove("active");
    document.getElementById("imperialBtn").classList.add("active");
    document.getElementById("metricSection").classList.remove("active");
    document.getElementById("imperialSection").classList.add("active");
    
    // Convert metric values to imperial if they exist
    const heightCm = parseFloat(document.getElementById("height").value) || 0;
    const weightKg = parseFloat(document.getElementById("weight").value) || 0;
    
    if (heightCm > 0) {
      const totalInches = heightCm / 2.54;
      const feet = Math.floor(totalInches / 12);
      const inches = (totalInches % 12);
      document.getElementById("heightFeet").value = feet;
      document.getElementById("heightInches").value = (Math.round(inches * 10) / 10).toFixed(1);
    }
    
    if (weightKg > 0) {
      const totalPounds = weightKg / 0.453592;
      const stone = Math.floor(totalPounds / 14);
      const pounds = (totalPounds % 14);
      document.getElementById("weightStone").value = stone;
      document.getElementById("weightPounds").value = (Math.round(pounds * 10) / 10).toFixed(1);
    }
  }

  document.getElementById("calorieForm").addEventListener("submit", function(e) {
    e.preventDefault();

    const gender = document.getElementById("gender").value;
    const age = parseFloat(document.getElementById("age").value);
    const activity = parseFloat(document.getElementById("activity").value);
    const goal = document.getElementById("goal").value;
    const macro = document.getElementById("macroSplit").value;

    let height, weight;

    // Check if we're using metric or imperial
    const isMetric = document.getElementById("metricSection").classList.contains("active");
    
    if (isMetric) {
      height = parseFloat(document.getElementById("height").value);
      weight = parseFloat(document.getElementById("weight").value);
    } else {
      // Convert imperial to metric
      const feet = parseFloat(document.getElementById("heightFeet").value) || 0;
      const inches = parseFloat(document.getElementById("heightInches").value) || 0;
      const stone = parseFloat(document.getElementById("weightStone").value) || 0;
      const pounds = parseFloat(document.getElementById("weightPounds").value) || 0;
      
      height = (feet * 12 + inches) * 2.54; // Convert to cm
      const totalPounds = stone * 14 + pounds;
      weight = totalPounds * 0.453592; // Convert to kg
    }

    // Enhanced validation with debug info
    console.log("Debug info:", {
      gender, age, activity, goal, macro, height, weight, isMetric
    });

    if (!gender || !age || !activity || !goal || !macro) {
      alert("Please fill in all required fields");
      return;
    }

    if (isNaN(height) || isNaN(weight) || height <= 0 || weight <= 0) {
      alert("Please enter valid height and weight values. Height: " + height + ", Weight: " + weight);
      return;
    }

    if (age <= 0 || age > 120) {
      alert("Please enter a valid age");
      return;
    }

    // Calculate BMR using Mifflin-St Jeor equation
    console.log("Calculating BMR with:", { gender, weight, height, age });
    let bmr = gender === "male"
      ? 10 * weight + 6.25 * height - 5 * age + 5
      : 10 * weight + 6.25 * height - 5 * age - 161;

    console.log("BMR:", bmr);
    const tdee = bmr * activity;
    console.log("TDEE:", tdee);

    function getMacros(calories) {
      let p = 0.3, c = 0.4, f = 0.3;
      if (macro === "highProtein") { p = 0.4; c = 0.3; f = 0.3; }
      else if (macro === "keto") { p = 0.25; c = 0.05; f = 0.7; }
      else if (macro === "vegan") { p = 0.25; c = 0.5; f = 0.25; }
      else if (macro === "paleo") { p = 0.35; c = 0.25; f = 0.4; }

      return {
        calories: Math.round(calories),
        protein: Math.round((calories * p) / 4),
        carbs: Math.round((calories * c) / 4),
        fats: Math.round((calories * f) / 9)
      };
    }

    const result = { maintenance: getMacros(tdee) };
    if (goal === "lose") result.loss_0_5kg = getMacros(tdee - 500);
    if (goal === "gain") {
      result.gain_0_5kg = getMacros(tdee + 500);
      result.gain_1kg = getMacros(tdee + 1000);
    }

    let html = `
      <h3>Maintenance Recommendation</h3>
      <p><strong>Calories:</strong> ${result.maintenance.calories}</p>
      <p>Protein: ${result.maintenance.protein}g | Carbs: ${result.maintenance.carbs}g | Fats: ${result.maintenance.fats}g</p>
    `;

    if (goal === "lose") {
      html += `
        <h3>Weight Loss</h3>
        <p><strong>0.5kg/week:</strong> ${result.loss_0_5kg.calories} kcal - P: ${result.loss_0_5kg.protein}g | C: ${result.loss_0_5kg.carbs}g | F: ${result.loss_0_5kg.fats}g</p>`;
    }

    if (goal === "gain") {
      html += `
        <h3>Weight Gain</h3>
        <p><strong>0.5kg/week:</strong> ${result.gain_0_5kg.calories} kcal - P: ${result.gain_0_5kg.protein}g | C: ${result.gain_0_5kg.carbs}g | F: ${result.gain_0_5kg.fats}g</p>
        <p><strong>1kg/week:</strong> ${result.gain_1kg.calories} kcal - P: ${result.gain_1kg.protein}g | C: ${result.gain_1kg.carbs}g | F: ${result.gain_1kg.fats}g</p>`;
    }

    const resultsDiv = document.getElementById("results");
    resultsDiv.innerHTML = html;
    resultsDiv.style.display = "block";

    // Show the disclaimer and email option button
    document.getElementById("disclaimer").style.display = "block";
    document.getElementById("emailPrompt").style.display = "block";
    
    // Scroll to results
    resultsDiv.scrollIntoView({ behavior: 'smooth' });
  });
</script>

</body>
</html>
