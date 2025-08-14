import tkinter as tk
from tkinter import messagebox
import random
import csv

# Load words from CSV
def load_words(filename='german_words&transaltions.csv'):
    words = []
    try:
        with open(filename, newline='', encoding='utf-8') as csvfile:
            reader = csv.reader(csvfile)
            for row in reader:
                # Ignore empty or malformed rows
                if len(row) == 2 and row[0].strip() and row[1].strip():
                    german = row[0].strip()
                    english = row[1].strip()
                    words.append((german, english))
    except FileNotFoundError:
        messagebox.showerror("File Not Found", f"Cannot find '{filename}'. Please make sure the file exists.")
    return words


class MatchingGame:
    def __init__(self, root):
        self.root = root
        self.root.title("German-English Word Match Game")
        self.all_words = load_words()
        self.selected_german = None
        self.selected_english = None
        self.current_pairs = []
        self.buttons_german = []
        self.buttons_english = []
        self.correct_matches = 0

        self.status_label = tk.Label(root, text="Click a German word, then its English translation", font=("Arial", 12))
        self.status_label.pack(pady=10)

        self.frame = tk.Frame(root)
        self.frame.pack()

        self.load_new_game()

    def load_new_game(self):
        for widget in self.frame.winfo_children():
            widget.destroy()

        if len(self.all_words) < 6:
            messagebox.showerror("Error", "Not enough word pairs in the CSV file (need at least 6).")
            self.root.quit()
            return

        self.selected_german = None
        self.selected_english = None
        self.correct_matches = 0

        self.current_pairs = random.sample(self.all_words, 6)
        german_words = [pair[0] for pair in self.current_pairs]
        english_words = [pair[1] for pair in self.current_pairs]
        random.shuffle(german_words)
        random.shuffle(english_words)

        self.buttons_german = []
        self.buttons_english = []

        for i, word in enumerate(german_words):
            btn = tk.Button(self.frame, text=word, width=20, height=2,
                            command=lambda w=word, b=i: self.select_word('german', w, b))
            btn.grid(row=i, column=0, padx=10, pady=5)
            self.buttons_german.append(btn)

        for i, word in enumerate(english_words):
            btn = tk.Button(self.frame, text=word, width=20, height=2,
                            command=lambda w=word, b=i: self.select_word('english', w, b))
            btn.grid(row=i, column=1, padx=10, pady=5)
            self.buttons_english.append(btn)

    def select_word(self, language, word, index):
        if language == 'german':
            self.selected_german = word
            self.highlight_button(self.buttons_german, index)
        else:
            self.selected_english = word
            self.highlight_button(self.buttons_english, index)

        if self.selected_german and self.selected_english:
            if self.is_correct_match(self.selected_german, self.selected_english):
                self.status_label.config(text="✅ Correct!")
                self.disable_pair(self.selected_german, self.selected_english)
                self.correct_matches += 1
                if self.correct_matches == 6:
                    messagebox.showinfo("Well done!", "You matched all pairs!")
                    self.load_new_game()
            else:
                self.status_label.config(text="❌ Incorrect. Try again.")
            self.selected_german = None
            self.selected_english = None
            self.clear_highlights()

    def is_correct_match(self, german, english):
        return (german, english) in self.current_pairs

    def disable_pair(self, german, english):
        for btn in self.buttons_german:
            if btn['text'] == german:
                btn.config(state='disabled', bg='lightgreen')
        for btn in self.buttons_english:
            if btn['text'] == english:
                btn.config(state='disabled', bg='lightgreen')

    def highlight_button(self, button_list, index):
        self.clear_highlights()
        button_list[index].config(bg='lightblue')

    def clear_highlights(self):
        for btn in self.buttons_german + self.buttons_english:
            if btn['state'] == 'normal':
                btn.config(bg='SystemButtonFace')

# --- Main Program ---
if __name__ == '__main__':
    root = tk.Tk()
    game = MatchingGame(root)
    root.mainloop()
