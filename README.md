import tkinter as tk
from tkinter import messagebox
import pandas as pd

# ฟังก์ชันสำหรับการล็อกอิน
def login():
    username = entry_username.get()
    password = entry_password.get()
    if username == "admin" and password == "password":
        messagebox.showinfo("Login Success", "Welcome Admin!")
        login_window.destroy()
        show_main_window()
    else:
        messagebox.showerror("Login Failed", "Invalid username or password")

# ฟังก์ชันสำหรับการแสดงหน้าต่างหลัก
def show_main_window():
    main_window = tk.Tk()
    main_window.title("Investment Risk Analysis")

    # ส่วนต่าง ๆ ของหน้าต่างหลัก
    tk.Label(main_window, text="Stock Name").grid(row=0, column=0)
    tk.Label(main_window, text="Stock Price (THB)").grid(row=1, column=0)
    tk.Label(main_window, text="Stock Price (USD)").grid(row=2, column=0)
    tk.Label(main_window, text="Exchange Rate").grid(row=3, column=0)
    tk.Label(main_window, text="Price Change Percent").grid(row=4, column=0)

    stock_name = tk.Entry(main_window)
    stock_price_thb = tk.Entry(main_window)
    stock_price_usd = tk.Entry(main_window)
    exchange_rate = tk.Entry(main_window)
    price_change_percent = tk.Entry(main_window)

    stock_name.grid(row=0, column=1)
    stock_price_thb.grid(row=1, column=1)
    stock_price_usd.grid(row=2, column=1)
    exchange_rate.grid(row=3, column=1)
    price_change_percent.grid(row=4, column=1)

    # ฟังก์ชันสำหรับการคำนวณ
    def calculate():
        thb = float(stock_price_thb.get())
        usd = float(stock_price_usd.get())
        rate = float(exchange_rate.get())
        percent = float(price_change_percent.get())
        daily_change = thb * (percent / 100)
        monthly_change = daily_change * 30
        messagebox.showinfo("Calculation Result", f"Daily Change: {daily_change:.2f} THB\nMonthly Change: {monthly_change:.2f} THB")

    tk.Button(main_window, text="Calculate", command=calculate).grid(row=5, column=1)
    
    main_window.mainloop()

# สร้างหน้าต่างล็อกอิน
login_window = tk.Tk()
login_window.title("Login")

tk.Label(login_window, text="Username").grid(row=0, column=0)
tk.Label(login_window, text="Password").grid(row=1, column=0)
entry_username = tk.Entry(login_window)
entry_password = tk.Entry(login_window, show='*')

entry_username.grid(row=0, column=1)
entry_password.grid(row=1, column=1)

tk.Button(login_window, text="Login", command=login).grid(row=2, column=1, pady=4)

login_window.mainloop()
