import tkinter as tk
from tkinter import messagebox
import re


# Function to validate the phone number (10 digits)
def validate_phone(phone):
    return re.match(r'^\d{10}$', phone)


# Function to validate email address
def validate_email(email):
    return re.match(r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$', email) is not None


# Function to clear the form after adding the employee
def add_employee():
    name = entry_name.get()
    phone = entry_phone.get()
    gender = gender_var.get()
    email = entry_email.get()

    # Validating input fields
    if name == "" or phone == "" or email == "" or gender == "":
        messagebox.showwarning("Input Error", "All fields must be filled out!")
        return

    # Validate phone number
    if not validate_phone(phone):
        messagebox.showwarning("Invalid Phone Number", "Phone number must be 10 digits long!")
        return

    # Validate email address
    if not validate_email(email):
        messagebox.showwarning("Invalid Email", "Please enter a valid email address!")
        return

    # Add your logic to save the employee data (e.g., to a file, database, etc.)
    print(f"Employee Added: {name}, {phone}, {gender}, {email}")

    # Show success message
    messagebox.showinfo("Success", f"Employee {name} added successfully!")

    # Clear the form for adding new employee
    entry_name.delete(0, tk.END)
    entry_phone.delete(0, tk.END)
    entry_email.delete(0, tk.END)
    gender_var.set("")


# Setting up the Tkinter window
window = tk.Tk()
window.title("Employee Registration Form")
window.geometry("400x400")

# Name Label and Entry
label_name = tk.Label(window, text="Name:")
label_name.pack(pady=5)
entry_name = tk.Entry(window, width=30)
entry_name.pack(pady=5)

# Phone Number Label and Entry
label_phone = tk.Label(window, text="Phone Number:")
label_phone.pack(pady=5)
entry_phone = tk.Entry(window, width=30)
entry_phone.pack(pady=5)

# Gender Label and Radio Buttons
label_gender = tk.Label(window, text="Gender:")
label_gender.pack(pady=5)

gender_var = tk.StringVar(value="")
radio_male = tk.Radiobutton(window, text="Male", variable=gender_var, value="Male")
radio_female = tk.Radiobutton(window, text="Female", variable=gender_var, value="Female")
radio_male.pack(pady=5)
radio_female.pack(pady=5)


label_email = tk.Label(window, text="Email Address:")
label_email.pack(pady=5)
entry_email = tk.Entry(window, width=30)
entry_email.pack(pady=5)


button_add = tk.Button(window, text="Add Employee", command=add_employee)
button_add.pack(pady=20)


window.mainloop()
