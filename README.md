function gradeCalc(grade, unit) {
if (grade === "S") {
return 10 * unit;
} else if (grade === "A") {
return 9 * unit;
} else if (grade === "B") {
return 8 * unit;
} else if (grade === "C") {
return 7 * unit;
} else if (grade === "D") {
return 6 * unit;
} else if (grade === "E") {
return 5 * unit;
}
}

let counter = 1;

function addCourse() {
let addNew = document.createElement("form");
addNew.classList.add("add_new", `key-${counter}`);
const course_name = `
<form class="add_new key-${counter}">
<input type="text" placeholder="Course Code" class="courses key-${counter}" required>
<input type="number" placeholder="Credit Unit" class="credit-units key-${counter}" required>
<select class="grade key-${counter}" required>
<option value="select">Select</option>
<option value="10">S</option>
<option value="9">A</option>
<option value="8">B</option>
<option value="7">C</option>
<option value="6">D</option>
<option value="5">E</option>
</select>
</form>
`;
addNew.innerHTML = course_name;
document.getElementById("course-wrapper").appendChild(addNew);
counter++;
}

function removeCourse() {
let mainForm = document.querySelector("form.add_new");
mainForm?.remove();
}

function calcCgpa() {
const CGPAPARAGRAPH = document.getElementById("cgpa-calc");
const PROGRESSBAR = document.getElementById("progress");

const GRADESSELECT = document.querySelectorAll("select.grade");
const UNIT = document.querySelectorAll("input.credit-units");

const courseReport = {};

const listOfGrades = [];
const listOfUnits = [];
let totalUnits = 0;

GRADESSELECT.forEach((e) => {
let GRADES = e.options;
const selectedIndex = e.selectedIndex;
const selectedGrade = GRADES[selectedIndex];
const gradeValue = selectedGrade.text.toUpperCase();
listOfGrades.push(gradeValue);
});

UNIT.forEach((e) => {
const unitValue = parseInt(e.value);
totalUnits += unitValue;
listOfUnits.push(unitValue);
});

let totalEarnedUnits = 0;

for (let i = 0; i < listOfUnits.length; i++) {
totalEarnedUnits += gradeCalc(listOfGrades[i], listOfUnits[i]);
}

const gpa = totalEarnedUnits / totalUnits;

if (gpa >= 0) {
CGPAPARAGRAPH.textContent = "Your CGPA is " + gpa.toFixed(2);

const percentage = (gpa / 10) * 100;
PROGRESSBAR.style.width = percentage + "%";
} else {
CGPAPARAGRAPH.textContent = "Please enter a valid grade and credit units";
PROGRESSBAR.style.width = "0";
}
}
function resetForm() {
const CGPAPARAGRAPH = document.getElementById("cgpa-calc");
const PROGRESSBAR = document.getElementById("progress");

// Reset CGPA and progress bar
CGPAPARAGRAPH.textContent = "Your CGPA is:";
PROGRESSBAR.style.width = "0";

// Reset input fields
const COURSES = document.querySelectorAll("input.courses");
const CREDIT_UNITS = document.querySelectorAll("input.credit-units");
const GRADES = document.querySelectorAll("select.grade");

COURSES.forEach((input) => (input.value = ""));
CREDIT_UNITS.forEach((input) => (input.value = ""));
GRADES.forEach((select) => (select.selectedIndex = 0));
}
