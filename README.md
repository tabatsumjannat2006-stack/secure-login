[design.py](https://github.com/user-attachments/files/30369155/design.py)
import tkinter as tk
from tkinter import messagebox

root = tk.Tk()
root.title("importUser Login UI")
root.geometry("400x550")
root.configure(bg="#4ba3e3")

# --- FUNCTIONAL BACKEND LOGIC ---
def handle_login():
    username = username_entry.get()
    password = password_entry.get()
    
    if username == "admin" and password == "1234":
        messagebox.showinfo("Success", "Welcome! Login Successful. 🎉")
        root.destroy() 
    elif username == "Username" or password == "Password" or not username or not password:
        messagebox.showwarning("Input Error", "Please fill out both fields.")
    else:
        messagebox.showerror("Error", "Invalid Username or Password! ❌")

# --- FORGOT PASSWORD FUNCTIONALITY ---
def open_forgot_password_window(event):
    # Create a new top-level pop-up window
    reset_win = tk.Toplevel(root)
    reset_win.title("Reset Password")
    reset_win.geometry("350x250")
    reset_win.configure(bg="#4ba3e3")
    
    # Inner elements for the reset window
    lbl = tk.Label(reset_win, text="Enter your registered Email:", font=("Arial", 11, "bold"), fg="#ffffff", bg="#4ba3e3")
    lbl.pack(pady=(30, 10))
    
    email_entry = tk.Entry(reset_win, font=("Arial", 12), width=25)
    email_entry.pack(pady=10)
    
    def submit_reset():
        email = email_entry.get()
        if "@" in email and "." in email: # Basic email check
            messagebox.showinfo("Reset Sent", f"A temporary reset link has been successfully sent to:\n{email}", parent=reset_win)
            reset_win.destroy()
        else:
            messagebox.showerror("Invalid Email", "Please enter a valid email address.", parent=reset_win)

    submit_btn = tk.Button(reset_win, text="Send Reset Link", font=("Arial", 11, "bold"), fg="#4ba3e3", bg="#ffffff", bd=0, command=submit_reset, cursor="hand2")
    submit_btn.pack(pady=20, ipady=4, ipadx=10)

# --- PLACEHOLDER FUNCTIONS ---
def clear_user_placeholder(event):
    if username_entry.get() == "Username":
        username_entry.delete(0, tk.END)

def restore_user_placeholder(event):
    if not username_entry.get():
        username_entry.insert(0, "Username")

def clear_pass_placeholder(event):
    if password_entry.get() == "Password":
        password_entry.delete(0, tk.END)
        password_entry.config(show="*")

def restore_pass_placeholder(event):
    if not password_entry.get():
        password_entry.config(show="")
        password_entry.insert(0, "Password")

# --- UI DESIGN ELEMENTS ---
main_frame = tk.Frame(root, bg="#4ba3e3")
main_frame.pack(expand=True, fill="both", padx=40, pady=40)

canvas = tk.Canvas(main_frame, width=120, height=120, bg="#4ba3e3", highlightthickness=0)
canvas.pack(pady=(10, 5))
canvas.create_oval(10, 10, 110, 110, fill="#74b9ef", outline="#ffffff", width=2)
canvas.create_oval(42, 25, 78, 61, fill="#ffffff", outline="")
canvas.create_arc(22, 65, 98, 130, start=0, extent=180, fill="#ffffff", outline="")

title_label = tk.Label(main_frame, text="USER LOGIN", font=("Arial", 18, "bold"), fg="#ffffff", bg="#4ba3e3")
title_label.pack(pady=(0, 25))

username_frame = tk.Frame(main_frame, bg="#ffffff", bd=0)
username_frame.pack(fill="x", pady=8, ipady=4)
user_icon = tk.Label(username_frame, text=" 👤 |", font=("Arial", 12), fg="#666666", bg="#ffffff")
user_icon.pack(side="left", padx=(10, 5))

username_entry = tk.Entry(username_frame, font=("Arial", 12), fg="#333333", bg="#ffffff", bd=0)
username_entry.insert(0, "Username")
username_entry.bind("<FocusIn>", clear_user_placeholder)
username_entry.bind("<FocusOut>", restore_user_placeholder)
username_entry.pack(side="left", fill="x", expand=True, padx=(0, 10))

password_frame = tk.Frame(main_frame, bg="#ffffff", bd=0)
password_frame.pack(fill="x", pady=8, ipady=4)
pass_icon = tk.Label(password_frame, text=" 🔒 |", font=("Arial", 12), fg="#666666", bg="#ffffff")
pass_icon.pack(side="left", padx=(10, 5))

password_entry = tk.Entry(password_frame, font=("Arial", 12), fg="#333333", bg="#ffffff", bd=0)
password_entry.insert(0, "Password")
password_entry.bind("<FocusIn>", clear_pass_placeholder)
password_entry.bind("<FocusOut>", restore_pass_placeholder)
password_entry.pack(side="left", fill="x", expand=True, padx=(0, 10))

options_frame = tk.Frame(main_frame, bg="#4ba3e3")
options_frame.pack(fill="x", pady=15)

remember_var = tk.BooleanVar(value=True)
remember_check = tk.Checkbutton(options_frame, text="Remember me", variable=remember_var, font=("Arial", 10), fg="#ffffff", bg="#4ba3e3", activebackground="#4ba3e3", activeforeground="#ffffff", selectcolor="#4ba3e3", bd=0)
remember_check.pack(side="left")

# Link label mapped to open_forgot_password_window action
forgot_label = tk.Label(options_frame, text="Forgot Password?", font=("Arial", 10, "italic"), fg="#dbeeff", bg="#4ba3e3", cursor="hand2")
forgot_label.pack(side="right")
forgot_label.bind("<Button-1>", open_forgot_password_window) # Binds left mouse click to function

login_btn = tk.Button(main_frame, text="LOGIN", font=("Arial", 14, "bold"), fg="#4ba3e3", bg="#ffffff", activebackground="#f0f0f0", activeforeground="#4ba3e3", bd=0, cursor="hand2", relief="flat", command=handle_login)
login_btn.pack(fill="x", pady=(20, 10), ipady=6)

root.mainloop()
