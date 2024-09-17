"""
██████╗░░█████╗░██╗░░░██╗
██╔══██╗██╔══██╗╚██╗░██╔╝
██████╦╝██║░░██║░╚████╔╝░
██╔══██╗██║░░██║░░╚██╔╝░░
██████╦╝╚█████╔╝░░░██║░░░
╚═════╝░░╚════╝░░░░╚═╝░░░
"""
#======================================================= Import ===============================================#

import math
import tkinter as tk
from time import sleep
try:
    from tkinter import *
except ImportError:    
    from tkinter import *

#======================================================= Set Window ===============================================#

window = tk.Tk()
window.title("Calculator")
window.minsize(width=400, height=400)
equation = StringVar()
equation1 = StringVar()
expression1=""
expression=""

#======================================================= Set Window ===============================================#

#======================================================= Def Number ===============================================#
def delete_number(delete):
    if (delete == "C"):
        global pop2
        global expression1
        global expression
        number_input.delete(0, END)
        number_input1.delete(0, END)
        title_entry1.delete(0, END)
        output_label.configure(text="")
        expression1=""
        expression=""
        equation.set("") 
        equation1.set("") 
        #print(pop2)

    elif (delete == "CE"):
        expression1=""
        equation1.set("")
        number_input1.delete(0, END)

def letter(letter):
    global number
    global number1
    global pop
    global pop1
    number = number_input.get()
    number1 = number_input.get()
    title_entry1.delete(0,END)
    if (letter == "pow"):
        pop1 = ""
        pop1 = pow(int(number),int(number1))
        title_entry1.insert(0,"x²")
        print(pop1)
    elif (number != ""):
        title_entry1.insert(0,str(letter))
        pop = (str(number) + (letter))
        #print(pop)

def equal():
    global number
    global number1
    global pop
    global pop1
    global letter1
    number = number_input.get()
    number1 = number_input1.get()
    letter1 = title_entry1.get()
    if (letter1 == "x²"):
        pop1 = ""
        pop1 = pow(int(number),int(number1))
        print(pop1)
    elif ((number != "")and(number1 != "")):
        pop = (str(number) + (letter1) + str(number1))
        pop1 = eval(pop)
    elif ((number == "")or(number1 == "")):
        output_label.configure(text="Please enter complete number.")
    output_label.configure(text=pop1)

def press(number):
    global expression
    global expression1
    letter1 = title_entry1.get()
    if (letter1 == ""):
        expression=expression + str(number)
        equation.set(expression) 
        print(expression)
    elif (letter1 != ""):      
        expression1=expression1+str(number)
        equation1.set(expression1) 
#======================================================= Def Number ===============================================#

#======================================================= Work Space ===============================================#

title_label = tk.Label(master=window, text= "Number",background="gray",width=19)
title_label.pack(pady=2)

number_input = tk.Entry(master=window,textvariable=equation,border=5,width=21,justify="center")
number_input.pack(pady=2)

title_entry1 = tk.Entry(master=window,border=5,width=21,justify="center")
title_entry1.pack(pady=2)

number_input1 = tk.Entry(master=window,textvariable=equation1,border=5,width=21,justify="center")
number_input1.pack(pady=2)

grid_frame = tk.Frame(window)
grid_frame.pack() 

#======================================================= Buttom Number ===============================================#

seven_button = tk.Button(grid_frame,text='7', bg = "gray", command=lambda:press("7"),width=5,).grid(row=0, column=0,columnspan=1)
eight_button = tk.Button(grid_frame,text='8', bg = "gray", command=lambda:press("8"),width=5,).grid(row=0, column=1,columnspan=1)
nine_button = tk.Button(grid_frame,text='9', bg = "gray", command=lambda:press("9"),width=5,).grid(row=0, column=2,columnspan=4)
four_button = tk.Button(grid_frame,text='4', bg = "gray", command=lambda:press("4"),width=5,).grid(row=1, column=0,columnspan=1)
five_button = tk.Button(grid_frame,text='5', bg = "gray", command=lambda:press("5"),width=5,).grid(row=1, column=1,columnspan=1)
six_button = tk.Button(grid_frame,text='6', bg = "gray", command=lambda:press("6"),width=5,).grid(row=1, column=2,columnspan=4)
one_button = tk.Button(grid_frame,text='1', bg = "gray", command=lambda:press("1"),width=5,).grid(row=2, column=0,columnspan=1)
two_button = tk.Button(grid_frame,text='2', bg = "gray", command=lambda:press("2"),width=5,).grid(row=2, column=1,columnspan=1)
three_button = tk.Button(grid_frame,text='3', bg = "gray", command=lambda:press("3"),width=5,).grid(row=2, column=2,columnspan=4)
zero_button = tk.Button(grid_frame,text='0', bg = "gray", command=lambda:press("0"),width=5,).grid(row=3, column=0,columnspan=1)

#======================================================= Buttom Number ===============================================#

#======================================================= Buttom Key ==================================================#

CE_button = tk.Button(grid_frame,text='CE', bg = "gray", command=lambda:delete_number("CE"),width=5,).grid(row=3, column=1,columnspan=1)
C_button = tk.Button(grid_frame,text='C', bg = "gray", command=lambda:delete_number("C"),width=5,).grid(row=3, column=2,columnspan=2)
plus_button = tk.Button(grid_frame,text='+',command=lambda:letter("+"),bg = "gray",width=5,).grid(row=4, column=0,)
delete_button = tk.Button(grid_frame,text='-',command=lambda:letter("-"),bg = "gray",width=5,).grid(row=4, column=1)
multiply_button = tk.Button(grid_frame,text='x',command=lambda:letter("*"),bg = "gray",width=5,).grid(row=4, column=2)
exponent_button = tk.Button(grid_frame,text='x²',command=lambda:letter("pow"),bg = "gray",width=5,).grid(row=5, column=2)
translate_button = tk.Button(grid_frame,text='/',command=lambda:letter("/"),bg = "gray",width=5,).grid(row=5, column=1)
dot_button = tk.Button(grid_frame,text='.',command=lambda:press("."),bg = "gray",width=5,).grid(row=5, column=0)
equal_button = tk.Button(master=window,text='=', bg = "gray",command=equal, width=18,)
equal_button.pack()

#======================================================= Buttom Key =================================================#

title_label = tk.Label(master=window, text= "Show answer",background="gray",width=19)
title_label.pack()

output_label = tk.Label(master=window,bg="gray",width=26,)
output_label.pack()

#======================================================= Work Space =================================================#

window.mainloop()
