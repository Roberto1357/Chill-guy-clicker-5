# Chill-guy-clicker-5
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chill Guy Clicker</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f0f0f0;
            margin: 0;
            padding: 0;
        }

        .container {
            margin: 50px auto;
            padding: 20px;
            max-width: 600px;
            background: #ffffff;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            position: relative; /* Für absolute Positionierung der Schaltflächen */
        }

        h1 {
            font-size: 2em;
            color: #333;
        }

        p {
            font-size: 1.5em;
            color: #666;
            margin: 20px 0;
        }

        #chillGuyContainer {
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }

        #chillGuy {
            width: 200px;
            height: auto;
            cursor: pointer;
            transition: transform 0.2s ease;
        }

        #chillGuy:active {
            transform: scale(1.1);
        }

        #upgradeButton {
            position: absolute;
            top: 20px;
            left: 20px;
            padding: 10px 20px;
            background-color: #4CAF50;
            color: white;
            font-size: 1.2em;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }

        #upgradeButton:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }

        #info {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Chill Guy Clicker</h1>
        <p>Klicks: <span id="clickCount">0</span></p>
        <p>Aktuelle Klicks pro Klick: <span id="clickMultiplier">1</span></p>
        <div id="chillGuyContainer">
            <!-- Bild des Chill Guy Memes -->
            <img id="chillGuy" src="https://i.postimg.cc/xjpCnZsV/IMG-9210.webp" alt="Chill Guy Meme">
        </div>

        <!-- Upgrade Button -->
        <button id="upgradeButton">Upgrade Kaufen</button>

        <div id="info">
            <p>Upgrade-Kosten: <span id="upgradeCost">10</span> Klicks</p>
        </div>
    </div>

    <script>
        let clickCount = 0; // Gesamtzahl der Klicks
        let clickMultiplier = 1; // Anzahl der Klicks pro Klick (Startwert 1)
        let upgradeCost = 10; // Startkosten für das erste Upgrade
        let upgradeLevel = 0; // Wie oft das Upgrade gekauft wurde

        // Referenzen zu den HTML-Elementen
        const clickCountElement = document.getElementById("clickCount");
        const clickMultiplierElement = document.getElementById("clickMultiplier");
        const chillGuy = document.getElementById("chillGuy");
        const upgradeButton = document.getElementById("upgradeButton");
        const upgradeCostElement = document.getElementById("upgradeCost");

        // Funktion: Erhöht den Klickzähler unter Berücksichtigung des Multiplikators
        function increaseClickCount() {
            clickCount += clickMultiplier; // Erhöht die Klicks je nach Multiplikator
            clickCountElement.textContent = clickCount;
        }

        // Funktion: Kauft ein Upgrade
        function buyUpgrade() {
            if (clickCount >= upgradeCost) {
                clickCount -= upgradeCost; // Klicks für das Upgrade abziehen
                upgradeLevel++; // Upgrade-Level erhöhen
                clickMultiplier = upgradeLevel + 1; // Erhöhe den Multiplikator (2 für das erste Upgrade, 3 für das zweite, etc.)
                upgradeCost = calculateNextUpgradeCost(); // Berechne die nächsten Upgrade-Kosten
                clickCountElement.textContent = clickCount;
                clickMultiplierElement.textContent = clickMultiplier;
                upgradeCostElement.textContent = upgradeCost;

                // Deaktiviere den Button, wenn genug Klicks für das nächste Upgrade vorhanden sind
                updateUpgradeButton();
            }
        }

        // Funktion: Berechnet die Kosten des nächsten Upgrades
        function calculateNextUpgradeCost() {
            // Steigere die Kosten für das Upgrade, die werden exponentiell ansteigen
            return Math.floor(upgradeCost * 1.5); // Upgrade-Kosten steigen um 50% nach jedem Kauf
        }

        // Funktion: Aktualisiert den Status des Upgrade-Buttons
        function updateUpgradeButton() {
            if (clickCount >= upgradeCost) {
                upgradeButton.disabled = false; // Button aktivieren
            } else {
                upgradeButton.disabled = true; // Button deaktivieren
            }
        }

        // Event Listener: Klick auf das Chill Guy Bild
        chillGuy.addEventListener("click", increaseClickCount);

        // Event Listener: Klick auf den Upgrade-Button
        upgradeButton.addEventListener("click", buyUpgrade);

        // Initialer Status des Upgrade-Buttons
        updateUpgradeButton();
    </script>
</body>
</html>
