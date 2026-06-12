# Treasury-App
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Alcohol Potency Comparator</title>

<style>
    body {
        font-family: Arial, sans-serif;
        margin: 30px;
        background: #f4f4f4;
    }

    .container {
        max-width: 800px;
        margin: auto;
        background: white;
        padding: 20px;
        border-radius: 10px;
    }

    h1 {
        text-align: center;
    }

    input, button {
        padding: 10px;
        margin: 5px;
    }

    table {
        width: 100%;
        border-collapse: collapse;
        margin-top: 20px;
    }

    th, td {
        border: 1px solid #ddd;
        padding: 10px;
        text-align: center;
    }

    th {
        background: #333;
        color: white;
    }

    .highest {
        background-color: #d4edda;
        font-weight: bold;
    }
</style>
</head>
<body>

<div class="container">
    <h1>Alcohol Potency Comparator</h1>

    <input type="text" id="label" placeholder="Brand / Label">
    <input type="number" id="abv" placeholder="ABV %" step="0.1">
    <button onclick="addAlcohol()">Add</button>

    <button onclick="sortByPotency()">Sort by Potency</button>

    <table>
        <thead>
            <tr>
                <th>Label</th>
                <th>ABV (%)</th>
            </tr>
        </thead>
        <tbody id="alcoholTable"></tbody>
    </table>
</div>

<script>
let alcohols = [];

function addAlcohol() {
    const label = document.getElementById("label").value;
    const abv = parseFloat(document.getElementById("abv").value);

    if (!label || isNaN(abv)) {
        alert("Enter a valid label and ABV.");
        return;
    }

    alcohols.push({
        label,
        abv
    });

    document.getElementById("label").value = "";
    document.getElementById("abv").value = "";

    renderTable();
}

function sortByPotency() {
    alcohols.sort((a, b) => b.abv - a.abv);
    renderTable();
}

function renderTable() {
    const table = document.getElementById("alcoholTable");
    table.innerHTML = "";

    const highestABV = Math.max(...alcohols.map(a => a.abv), 0);

    alcohols.forEach(item => {
        const row = document.createElement("tr");

        if (item.abv === highestABV) {
            row.classList.add("highest");
        }

        row.innerHTML = `
            <td>${item.label}</td>
            <td>${item.abv}%</td>
        `;

        table.appendChild(row);
    });
}
</script>

</body>
</html>