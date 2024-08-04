# -------------------------------------------------------
#                Python Tic Tac Toe game
# -------------------------------------------------------

from tkinter import *
import random

#Creating Game Body
window = Tk()
window.title("Tic Tac Toe")     #Header
players = ["X","O"]           
player = random.choice(players)
buttons = [[0,0,0],
           [0,0,0],
           [0,0,0]]

class Tic_Tac_Toe:
    def __init__(self, master):
        #Set Heading of the game
        self.label = Label(text=player + " Turn", font=("Courier New",40))
        self.label.pack(side="top")       
        
        #Creating Restart Button
        self.reset_button = Button(text="Restart", font=("Courier New",20), command=self.new_game)
        self.reset_button.pack(side="top")
        
        #Setting frame
        frame = Frame(master)
        frame.pack()

        #Create buttons 
        for row in range(3):
            for column in range(3):
                buttons[row][column] = Button(frame, text="", font=("Courier New",40), height=2, width=5,
                                              command = lambda row=row, column=column: self.next_turn(row, column))
                buttons[row][column].grid(row=row, column=column)



    def next_turn(self, row, column):    #For Next Turn

        global player

        if buttons[row][column]['text'] == "" and self.check_winner() is False:

            if player == players[0]:

                buttons[row][column]['text'] = player

                if self.check_winner() is False:
                    player = players[1]
                    self.label.config(text=(players[1]+" Turn"))

                elif self.check_winner() is True:
                    self.label.config(text=(players[0]+" Wins"))

                elif self.check_winner() == "Tie":
                    self.label.config(text="Tie!")

            else:

                buttons[row][column]['text'] = player

                if self.check_winner() is False:
                    player = players[0]
                    self.label.config(text=(players[0]+" Turn"))

                elif self.check_winner() is True:
                    self.label.config(text=(players[1]+" Wins"))

                elif self.check_winner() == "Tie":
                    self.label.config(text="Tie!")
    
    
    def check_winner(self):       #For checking if the user is win or not
        for row in range(3):
            if buttons[row][0]["text"] == buttons[row][1]["text"] == buttons[row][2]["text"] != "" :
                buttons[row][0].config(bg="green")
                buttons[row][1].config(bg="green")
                buttons[row][2].config(bg="green")
                return True

        for column in range(3):
            if buttons[0][column]["text"] == buttons[1][column]["text"] == buttons[2][column]["text"] != "" :
                buttons[0][column].config(bg="green")
                buttons[1][column].config(bg="green")
                buttons[2][column].config(bg="green")
                return True

        if buttons[0][0]["text"] == buttons[1][1]["text"] == buttons[2][2]["text"] != "" :
            buttons[0][0].config(bg="green")
            buttons[1][1].config(bg="green")
            buttons[2][2].config(bg="green")
            return True

        elif buttons[0][2]["text"] == buttons[1][1]["text"] == buttons[2][0]["text"] != "" :
            buttons[0][2].config(bg="green")
            buttons[1][1].config(bg="green")
            buttons[2][0].config(bg="green")
            return True

        elif self.empty_space() is False:
        
            for row in range(3):
                for column in range(3):
                    buttons[row][column].config(bg='Yellow')
        
            return "Tie"

        else:
            return False
        
    
    def empty_space(self):        #For checking empty space
    
        spaces = 9

        for row in range(3):
            for column in range(3):
                if buttons[row][column]['text'] != "" :
                    spaces -= 1

        if spaces == 0:
            return False

        else:
            return True

    
    def new_game(self):       #For new game
    
        global player

        player = random.choice(players)

        self.label.config(text=player + " Turn")

        for row in range(3):
            for column in range(3):
                buttons[row][column].config(text="", bg="#F0F0F0")
                

#Calling Method 
game = Tic_Tac_Toe(window)
window.mainloop()