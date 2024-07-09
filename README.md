# 1st-Tkinter-application-work-app-

'''Author: Anthony Lovato
Date written: 06/29/24
Assignment: M08 Project GUI Tkinter:
Short Desc: Program for "Employee service application".'''

from tkinter import *

"This is to initiate immediately and create the window and function for the login page."
#Main start-up window, with function that automatically leads to login page.
global login_window
login_window = Tk()
login_window.title("Login to Employee Work App")
login_window.geometry('840x540')
login_window.config(background ='#444444')

global logo_image
logo_image = PhotoImage(file='C:/Users/Alova/Pictures/Screenshots/earthpic.png')
login_window.iconphoto(True,logo_image)

"This is the section for the account page on the start-up window."
#Function for switching frames from the login page to the account page on start-up window, 
#with conditions if pass/username is correct.
def account_page():
    username = "Alovato"
    password = "swordfish"
    global account_frame
    account_frame = Frame(bg ='#444444')
    account_frame.pack()
    if username_entry.get() == username and password_entry.get() == password:
        main_frame.forget()
        account_frame.tkraise
        login_window.title("Employee Work App Home")        
#Frame for home page buttons and labels.
        account_label = Label(account_frame, text = "Welcome", bg = '#444444', fg = '#9e8c00', font = ("Arial", 30))
        employee_name = Label(account_frame, text = "Name:    A. Lovato", bg = '#444444', fg = 'white', font = ("Arial", 18))
        position = Label(account_frame, text = "Position:    Mechanic", bg = '#444444', fg = 'white', font = ("Arial", 18))
        department = Label(account_frame, text = "Department:    Carpentry", bg = '#444444', fg = 'white', font = ("Arial", 18))
        idnum = Label(account_frame, text = "ID#:    254698", bg = '#444444', fg = 'white', font = ("Arial", 18))
#Button(s).
        global logout_button
        logout_button = Button(account_frame, text = "logout", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                               command = lambda: reset())
        global timesheet_button
        timesheet_button = Button(account_frame, text = "Timesheet", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                                  command = lambda: timesheet_window())
#Placement for the labels and buttons.
        account_label.pack(side = 'top', fill = 'both', pady = 20)
        employee_name.pack(side = 'top', fill = 'both')
        position.pack(side = 'top', fill = 'both')
        department.pack(side = 'top', fill = 'both')
        idnum.pack(side = 'top', fill = 'both')
        timesheet_button.pack(side = 'top', fill = 'both')
        logout_button.pack(side = 'top', pady = 120)

    else:
        error_msg = Label(main_frame, text = "Incorrect username and/or password,\n" "please try again", 
                          bg = '#444444', fg = 'white', font = ("Arial", 18))
        error_msg.grid(row = 4, column = 0, columnspan = 2, pady = 40)

"This function is for the logout button, it removes the frame and initiates the login page."
def reset():
    account_frame.forget()
    login_page()

"This function is for the login page, the basic login style page."
def login_page():

    global main_frame
    main_frame = Frame(background ='#444444')
    main_frame.pack()
    
    login_label = Label(main_frame, text = "Login to Employee Work App", bg = '#444444', fg = '#9e8c00', font = ("Arial", 30))
    username_label = Label(main_frame, text = "Username", bg = '#444444', fg = 'white', font = ("Arial", 18))
    password_label = Label(main_frame, text = "Password", bg = '#444444', fg = 'white', font = ("Arial", 18))
    global username_entry
    username_entry = Entry(main_frame, font = ("Arial", 18))
    global password_entry
    password_entry = Entry(main_frame, font = ("Arial", 18))
    login_button = Button(main_frame, text = "login", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                          command = lambda: account_page())

#Place the widgets on the screen for the login window.
    login_label.grid(row = 0, column = 0, columnspan = 2, sticky = "news", pady = 40)
    username_label.grid(row = 1, column = 0)
    username_entry.grid(row = 1, column = 1, pady = 20)
    password_label.grid(row = 2, column = 0)
    password_entry.grid(row = 2, column = 1, pady = 20)
    login_button.grid(row = 3, column = 0, columnspan = 2, pady = 30)

def timesheet_window():
    global win
    win = Toplevel()
    win.title("Timesheet")
    win.geometry('840x540')
    win.config(background ='#444444')
    
    global ts_frame
    ts_frame = Frame(win, background ='#444444')
    ts_frame.pack()
    
    timesheet_label = Label(ts_frame, text = "Schedule", bg = '#444444', fg = '#9e8c00', font = ("Arial", 25))
    
    monday = Label(ts_frame, text = "Mon:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    tuesday = Label(ts_frame, text = "Tues:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    wednesday = Label(ts_frame, text = "Wed:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    thursday = Label(ts_frame, text = "Thur:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    friday = Label(ts_frame, text = "Fri     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    saturday = Label(ts_frame, text = "Sat:     --", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    sunday = Label(ts_frame, text = "Sun:     --", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    
    global button_msg
    button_msg = Label(ts_frame, text = "!", bg = '#444444', fg = 'white', font = ("Arial", 18))
    
#Buttons for the timesheet page.
    global clockin_button
    clockin_button = Button(ts_frame, text = "Clock-In", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                            command = lambda: clocking_in())
    global clockout_button
    clockout_button = Button(ts_frame, text = "Clock-Out", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                             command = lambda: clocking_out())
    global service_req_button
    service_req_button = Button(ts_frame, text = "Service Request", bg = '#9e8c00', fg = 'white', font = ("Arial", 12),
                                command = lambda: ser_req_page())
    
    timesheet_label.pack(side = 'top', pady=10)
    monday.pack(side = 'top')
    tuesday.pack(side = 'top')
    wednesday.pack(side = 'top')
    thursday.pack(side = 'top')
    friday.pack(side = 'top')
    saturday.pack(side = 'top')
    sunday.pack(side = 'top')
    
    clockin_button.pack(side = 'bottom', pady = 15)
    clockout_button.pack(side = 'bottom', pady = 15)
    service_req_button.pack(side = 'bottom', pady = 35)
    win.mainloop()
    
def clocking_in():
    button_msg['text'] = 'Clocked In!'
    button_msg.pack(side = 'bottom')
    
def clocking_out():
    button_msg['text'] = 'Clocked Out!'
    button_msg.pack(side = 'bottom')
    
def ser_req_page():
    ts_frame.forget()
    service_page()
    
def service_page():
    global service_frame
    service_frame = Frame(win, background ='#444444')
    service_frame.pack()
    
    service_request_label = Label(service_frame, text = "Please describe what request you would like to submit.", 
                                  bg = '#9e8c00', fg = 'white', font = ("Arial", 20))
    service_request_label.pack(side = 'top')

    win.mainloop()

login_page()
login_window.mainloop()
