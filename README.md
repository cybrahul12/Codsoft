import tkinter as tk
from tkinter import messagebox

def update_display(value):
    current = entry_display.get()
    if value == 'C':
        entry_display.delete(0, tk.END)
    elif value == '=':
        try:
            result = eval(current)
            entry_display.delete(0, tk.END)
            entry_display.insert(0, str(result))
        except Exception as e:
            messagebox.showerror("Error", "Invalid input")
    else:
        entry_display.insert(tk.END, value)

root = tk.Tk()
root.title("Simple Calculator")
root.configure(background='#FFCCCC')  # Light red background color

entry_display = tk.Entry(root, width=30, font=('Arial', 14), bd=5, relief=tk.RIDGE)
entry_display.grid(row=0, column=0, columnspan=4, padx=10, pady=10)

buttons = [
    '7', '8', '9', '/',
    '4', '5', '6', '*',
    '1', '2', '3', '-',
    '0', '.', '=', '+',
    'C'
]

row = 1
col = 0
for button in buttons:
    if button in ['/', '*', '-', '+']:
        tk.Button(root, text=button, width=5, height=2, command=lambda b=button: update_display(b)).grid(row=row, column=col, padx=5, pady=5)
        col += 1
    else:
        tk.Button(root, text=button, width=5, height=2, command=lambda b=button: update_display(b)).grid(row=row, column=col, padx=5, pady=5)
        col += 1
    if col > 3:
        col = 0
        row += 1

root.mainloop()
