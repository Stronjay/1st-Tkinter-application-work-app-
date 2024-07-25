'''Author: Anthony Lovato
Date written: 07/09/24
Assignment: M06 Project GUI Tkinter:
Short Desc: Program for "Employee service application".'''

from tkinter import *
from PIL import Image

#Create main window.
global login_window
login_window = Tk()
login_window.title("Login to Employee Work App")
login_window.geometry('940x640')
login_window.config(bg = '#444444')        

#Create 1st background image.
bg_image_def = PhotoImage(file='C:/Users/Alova/Pictures/Screenshots/office_image.png')
#Create 2nd background image.
rnb_image_def = PhotoImage(file='C:/Users/Alova/Pictures/Screenshots/rnb_image.png')
#Create top left icon image.
global logo_image
logo_image = PhotoImage(file='C:/Users/Alova/Pictures/Screenshots/earthpic.png')
login_window.iconphoto(True,logo_image)

#Account Frame and login credentials.
def account_page():
    username = "Alovato"
    password = "swordfish"
    global account_frame
    account_frame = Frame(bg = '#444444')
    account_frame.pack()
    global btm_account_frame
    btm_account_frame = Frame(bg = '#444444')
    btm_account_frame.pack()
#global the variable text for future use in gathering the entry for the service requests page.
    global text
#Code stored for req made page to have text display on frame.
    text = "No current requests have been made."
#-----------------------------------------------------------------main-frame->-account-frame----------------------------"
#Validate login credentials.
    if username_entry.get() == username and password_entry.get() == password:
        my_canvas.forget()
        account_frame.tkraise
        login_window.title("Employee Work App Home")  
#Account frame widgets.
        account_label = Label(account_frame, text = "Welcome", bg = '#444444', fg = '#9e8c00', font = ("Arial", 30))
        employee_name = Label(account_frame, text = "Name:    A. Lovato", bg = '#444444', fg = 'white', font = ("Arial", 18))
        position = Label(account_frame, text = "Position:    Manager", bg = '#444444', fg = 'white', font = ("Arial", 18))
        department = Label(account_frame, text = "Department:    Management", bg = '#444444', fg = 'white', font = ("Arial", 18))
        idnum = Label(account_frame, text = "ID#:    254698", bg = '#444444', fg = 'white', font = ("Arial", 18))
        spacing = Label(account_frame, text = "", bg = '#444444', fg = 'white', font = ("Arial", 18))
#Account frame buttons.
        global logout_button
        logout_button = Button(account_frame, text = "logout", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                               command = lambda: reset())
        global timesheet_button
        timesheet_button = Button(account_frame, text = "Timesheet Window", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                                  command = lambda: timesheet_window())
        global services_requested
        services_requested = Button(account_frame, text = "Requests Made", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                                command = lambda: records())
#Placement for all of the widgets on the Account frame.
        account_label.pack(pady=10)
        employee_name.pack(pady=10)
        position.pack(pady=10)
        department.pack(pady=10)
        idnum.pack(pady=10)
        spacing.pack(pady=10)
        timesheet_button.pack(pady=10)
        services_requested.pack(pady=10)
        logout_button.pack(pady=10)

#Create Canvas for background image
        global my_account_canvas
        my_account_canvas = Canvas(account_frame)
        my_account_canvas.pack(fill = 'both', expand = True)
#Set canvas image
        my_account_canvas.create_image(0,0, image = rnb_image_def, anchor = 'nw')
    
    else:
        my_canvas.create_text(500, 400, text = "Incorrect username and/or password,\n" "     please try again", 
                              font = ("Arial", 18), fill = 'black')
"--------------------------------------------------------account-frame->-login-page----------------------------------------------"
#Remove account frame and bring back the login frame.
def reset():
    account_frame.forget()
    login_page()

#Create the login page.
def login_page():
#Create Canvas for background image
    global my_canvas
    my_canvas = Canvas(login_window, width=940, height=640)
    my_canvas.pack(fill = 'both', expand=True)
#Set canvas image
    my_canvas.create_image(0,0, image = bg_image_def, anchor = 'nw')
#Create texts for the canvas.
    my_canvas.create_text(500, 50, text = "Login to Employee Work App", font = ("Arial", 30), fill = '#9e8c00')
    my_canvas.create_text(200, 150, text = "Username", font = ("Arial", 30), fill = '#9e8c00')
    my_canvas.create_text(200, 215, text = "Password", font = ("Arial", 30), fill = '#9e8c00')
#Add buttons and entries to the canvas.
    login_button = Button(login_window, text = "Login", bg = 'gray', fg = 'yellow', font = ("Arial", 12), command = lambda: account_page())
    global username_entry
    username_entry = Entry(login_window, font = ("Arial", 18))
    global password_entry
    password_entry = Entry(login_window, font = ("Arial", 18))
#place buttons for the canvas.
    global login_btn_window
    login_btn_window = my_canvas.create_window(450, 300, anchor="nw", window = login_button)
    global username_window
    username_window = my_canvas.create_window(370, 140, anchor="nw", window = username_entry)
    global password_window
    password_window = my_canvas.create_window(370, 200, anchor="nw", window = password_entry)
    global records

#Create a new (2nd) window for the timesheet.
def timesheet_window():
    global win
    win = Toplevel()
    win.title("Timesheet")
    win.geometry('840x540')
    win.config(background ='#444444')
    global ts_frame_func

#Create timesheet frame.
    def ts_frame_func():
        global ts_frame
        ts_frame = Frame(win, background ='#444444')
        ts_frame.pack()

#Create widgets for the timesheet frame.
        timesheet_label = Label(ts_frame, text = "Schedule", bg = '#444444', fg = '#9e8c00', font = ("Arial", 25))
        monday = Label(ts_frame, text = "Mon:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
        tuesday = Label(ts_frame, text = "Tues:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
        wednesday = Label(ts_frame, text = "Wed:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
        thursday = Label(ts_frame, text = "Thur:     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
        friday = Label(ts_frame, text = "Fri     9:00am-5:00pm", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
        saturday = Label(ts_frame, text = "Sat:     --", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
        sunday = Label(ts_frame, text = "Sun:     --", bg = '#444444', fg = '#9e8c00', font = ("Arial", 15))
    
#Create a place for the "Clocked-out!", "Clocked-in!", widget/text and only place it once the corresponding button is pressed.
        global button_msg
        button_msg = Label(ts_frame, text = "!", bg = '#444444', fg = 'white', font = ("Arial", 18))
    
#timesheet buttons.
        global clockin_button
        clockin_button = Button(ts_frame, text = "Clock-In", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                                command = lambda: clocking_in())
        global clockout_button
        clockout_button = Button(ts_frame, text = "Clock-Out", bg = '#9e8c00', fg = 'white', font = ("Arial", 12), 
                                 command = lambda: clocking_out())
        global service_req_button
        service_req_button = Button(ts_frame, text = "Make Service Request", bg = '#9e8c00', fg = 'white', font = ("Arial", 12),
                                    command = lambda: ser_req_page())

#Placement for the widgets in the timesheet page.
        timesheet_label.pack(side = 'top', pady=10)
        monday.pack(side = 'top')
        tuesday.pack(side = 'top')
        wednesday.pack(side = 'top')
        thursday.pack(side = 'top')
        friday.pack(side = 'top')
        saturday.pack(side = 'top')
        sunday.pack(side = 'top')
        clockin_button.pack(side = 'bottom', pady = 10)
        clockout_button.pack(side = 'bottom', pady = 10)
        service_req_button.pack(side = 'bottom', pady = 10)
    ts_frame_func()
    win.mainloop()
#------------------------------------------------------------------------------------------------------------
#Create function for text display when clocking in.
def clocking_in():
    button_msg['text'] = 'Clocked In!'
    button_msg.pack(side = 'bottom')
    
#Create function for text display when clocking out.
def clocking_out():
    button_msg['text'] = 'Clocked Out!'
    button_msg.pack(side = 'bottom')
"--------------------------------------------------------------------timesheet-frame->-service-frame-----------"
#Remove timesheet frame and initiate the service page(service_frame).
def ser_req_page():
    ts_frame.forget()
    service_page()

#Service page for making requests.
def service_page():
    global service_frame
    service_frame = Frame(win, background ='#444444')
    service_frame.pack()
    global submit

#Widgets for the service_frame.
    service_request_label = Label(service_frame, text = "Please describe the request you would like to submit.", 
                                  bg = '#444444', fg = 'white', font = ("Arial", 20))
    global service_entry
    service_entry = Entry(service_frame, width = 25, font = ("Arial", 26))

#Buttons for the service_frame.
    submit_btn = Button(service_frame, text = "Submit", bg = '#9e8c00', fg = 'white', font = ("Arial", 18),
                        command = lambda: submit())
    go_back1_btn = Button(service_frame, text = "Go Back", bg = '#9e8c00', fg = 'white', font = ("Arial", 18),
                          command = lambda: reset3())
#Placing widgets on the service_frame.
    service_request_label.grid(row=0, column=0, pady=25)
    service_entry.grid(row=1, column=0, pady=50)
    submit_btn.grid(row=2, column=0, pady=45)
    go_back1_btn.grid(row=3, column=0, pady=20)
    win.mainloop()
"-------------------------------------------------------------service-frame->-timesheet-frame----------------------------------"
#Remove service_frame and bring back the timesheet_frame.
def reset3():
    service_frame.forget()
    ts_frame_func()
    
#Clear text box and save users input.
global submit
def submit():
    global text
    text = service_entry.get()
    service_entry.delete(0, 'end')
    submit_label = Label(service_frame, text = "Submitted.", 
                     bg = '#444444', fg = 'white', font = ("Arial", 20))
    submit_label.grid(row=4, column=0, pady =20)
    
#Remove account frame and create new record frame that displays input from the service frame.
"-------------------------------------------------------account-frame->-record_frame------------------------------"
global records
def records():
    account_frame.forget()
    global record_frame
    record_frame = Frame(bg = '#444444')
    record_frame.pack()
    record_frame.tkraise

#Widgets for the record_frame.
    services_requested_label = Label(record_frame, text = "Requests submitted", 
                                     bg = '#444444', fg = 'white', font = ("Arial", 20))
    service_req_record = Label(record_frame, text = text, 
                                   bg = 'white', fg = 'black', font = ("Arial", 15))
    
#Back button for the record_frame.
    go_back = Button(record_frame, text = "Go Back", bg = '#9e8c00', fg = 'white', font = ("Arial", 18),
                        command = lambda: reset2())

#Placement for the wigets and the back button.
    services_requested_label.grid(row=0, column=0, pady =25)
    service_req_record.grid(row=1, column=0, pady =20)
    go_back.grid(row=2, column=0, pady=95)

#remove record_frame and bring back the Account page.
"----------------------------------------------------record-frame->-account-frame---------------------------------"
def reset2():
    record_frame.forget()
    account_page()

login_page()
login_window.mainloop()
