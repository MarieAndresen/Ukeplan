<!DOCTYPE html>
<html>
<head>
<title>Min ukedagsplan</title>
<style>
body {
font-family: 'Comic Sans MS', cursive, sans-serif;
margin: 20px;
background-color: #f9f9f9;
}
h1 {
color: blue;
text-align: center;
}
.dag {
border: 2px solid black;
margin: 10px;
padding: 10px;
background-color: #e6f7ff;
border-radius: 10px;
}
.del {
margin: 5px;
padding: 10px;
background-color: white;
border-radius: 5px;
}
.checkbox {
margin-right: 10px;
}
textarea {
width: 100%;
height: 60px;
margin-top: 5px;
font-family: 'Comic Sans MS', cursive, sans-serif;
}
button {
background-color: #4CAF50;
color: white;
border: none;
padding: 5px 10px;
border-radius: 5px;
cursor: pointer;
}
</style>
</head>
<body>
<h1>📅 Min ukedagsplan</h1>
<button onclick="clearAll()">Nullstill alt</button>

<div class="dag" id="mandag">
<h2>Mandag</h2>
<div class="del">
<h3><input type="checkbox" class="checkbox" id="mandag-morgen-check"> Morgen </h3>
<textarea id="mandag-morgen-text" placeholder="Hva skal du gjøre om morgenen?"></textarea>
</div>
<div class="del">
<h3><input type="checkbox" class="checkbox" id="mandag-ettermiddag-check"> Ettermiddag </h3>
<textarea id="mandag-ettermiddag-text" placeholder="Hva skal du gjøre om ettermiddagen?"></textarea>
</div>
<div class="del">
<h3><input type="checkbox" class="checkbox" id="mandag-kveld-check"> Kveld </h3>
<textarea id="mandag-kveld-text" placeholder="Hva skal du gjøre om kvelden?"></textarea>
</div>
</div>

<!-- Tirsdag til søndag -->

<script>
// Lagrer data når noe endres
document.querySelectorAll("textarea, input[type='checkbox']").forEach(element => {
element.addEventListener("input", saveData);
});

// Lagrer alt i Local Storage
function saveData() {
const allData = {};
document.querySelectorAll("textarea, input[type='checkbox']").forEach(element => {
if (element.type === "checkbox") {
allData[element.id] = element.checked;
} else {
allData[element.id] = element.value;
}
});
localStorage.setItem("ukedagsplan", JSON.stringify(allData));
}

// Laster inn lagret data
function loadData() {
const savedData = localStorage.getItem("ukedagsplan");
if (savedData) {
const allData = JSON.parse(savedData);
Object.keys(allData).forEach(id => {
const element = document.getElementById(id);
if (element) {
if (element.type === "checkbox") {
element.checked = allData[id];
} else {
element.value = allData[id];
}
}
});
}
}

// Nullstill alt
function clearAll() {
if (confirm("Er du sikker på at du vil slette alt?")) {
localStorage.removeItem("ukedagsplan");
document.querySelectorAll("textarea").forEach(box => box.value = "");
document.querySelectorAll("input[type='checkbox']").forEach(box => box.checked = false);
}
}

// Last inn data når siden åpnes
window.onload = loadData;
</script>
</body>
</html>

