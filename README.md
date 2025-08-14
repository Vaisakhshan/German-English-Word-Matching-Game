# German-English Word Matching Game 🇩🇪➡️🇬🇧

A simple **Tkinter-based Python game** to help you learn German vocabulary by matching German words with their English translations.  
The game loads words from a CSV file, displays them in two columns, and lets you match them by clicking the correct pairs.  

---

## ✨ Features
- Loads word pairs from a **CSV file** (`trennbare_verben_1.csv` by default).
- Randomly selects 6 pairs per round.
- Interactive **GUI with Tkinter**.
- Highlights selected words and marks correct matches in green.
- Displays feedback on correct/incorrect attempts.
- Automatically starts a new game when all pairs are matched.

---

## 📂 CSV File Format
The CSV file must contain **two columns**:
```csv
German,English
aufstehen,to get up
anrufen,to call
...

