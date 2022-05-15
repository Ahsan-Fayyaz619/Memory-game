# Memory-game
Just use the link to run the code

from tkinter import *
from tkinter import ttk
import random
import time

window = Tk()
window.title('Memory Game')
window.minsize(height = 650, width = 650)

progress_bar = ttk.Progressbar(window, orient = HORIZONTAL, length = 500, mode = 'determinate')
progress_bar.pack(pady = 150)

def bar():
    progress_bar['value'] = 10
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 20
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 30
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 40
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 50
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 60
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 70
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 80
    window.update_idletasks()
    time.sleep(.1)
    progress_bar['value'] = 90
    window.update_idletasks()
    time.sleep(.5)
    load_name.destroy()
    progress_bar.destroy()
    start_button.destroy()
    main_window()

load_name = Label(window, text=' Loading... ', font=('Baskerville', 17))
load_name.pack()
start_button = Button(window, text=' START ', font=('Baskerville', 20), foreground='Crimson', command = bar)
start_button.pack()

def main_window():
    def easy_window():
        intro.destroy()
        names.destroy()
        easy.destroy()
        medium.destroy()
        hard.destroy()
        window.title("Easy Level")

        easy_level()

    def medium_window():
        intro.destroy()
        names.destroy()
        easy.destroy()
        medium.destroy()
        hard.destroy()
        window.title("Medium Level")

        medium_level()

    def hard_window():
        intro.destroy()
        names.destroy()
        easy.destroy()
        medium.destroy()
        hard.destroy()
        window.title("Hard Level")

        hard_level()

    intro = Label(window, text='\n\n\n\nWelcome to the Memory Game!\n\nChoose Your Level!\n\n\n',
                  font = ('Baskerville', 30), foreground = 'Black')
    intro.pack()
    names = Label(window, text = 'Designed by Fatima, Ahsan & Zarak\nas part of our PFUN Final Project',
                  font = ('Baskerville', 15), foreground = 'Black')
    names.pack(side = BOTTOM)
    easy = Button(window, text = 'Easy', font = ('Baskerville', 20), foreground = 'Crimson', command = easy_window)
    easy.pack()
    medium = Button(window, text = 'Medium', font = ('Baskerville', 20), foreground = 'Crimson', command=medium_window)
    medium.pack()
    hard = Button(window, text = 'Hard', font = ('Baskerville', 20), foreground = 'Crimson', command = hard_window)
    hard.pack()

# For All levels
moves = IntVar()
moves = 0
begin_time = 0
# Level 1 and 2
prev_1 = [100, 100]
# Level 3
prev_2 = [80, 80]


# Level 1 Code
def easy_level():
    global begin_time
    begin_time = time.time()
    create = Canvas(width = 500, height = 500)
    create.pack()

    board = [list('.' * 4) for count in range(4)]
    ans = list('AABBCCDDEEFFGGHH')
    random.shuffle(ans)
    ans = [ans[:4],
           ans[4:8],
           ans[8:12],
           ans[12:]]

    def draw(x, y, z):
        if x == 'A':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Red', outline='Black')
        elif x == 'B':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Green', outline='Black')
        elif x == 'C':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Blue', outline='Black')
        elif x == 'D':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='Yellow', outline='Black')
        elif x == 'E':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='Brown', outline='Black')
        elif x == 'F':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='Orange', outline='Black')
        elif x == 'G':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20, 100 * z + 100 - 20, fill='Purple', outline='Black')
        elif x == 'H':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20, 100 * z + 100 - 20, fill='Pink', outline='Black')

    def quiz_board():
        global begin_time
        count = 0
        # time = 0
        for i in range(4):
            for j in range(4):
                rec = create.create_rectangle(100 * i, j * 100, 100 * i + 100, 100 * j + 100, fill='Light Grey')
                if (board[i][j] != '.'):
                    draw(board[i][j], i, j)
                    count += 1
        if count == 16:
            # moves
            create.create_text(200, 425, text = 'CONGRATULATIONS!!!\n You finished the game in:', font=('Baskerville', 17))
            create.create_text(200, 455, text = str(moves) + ' moves', font=('Baskerville', 17))
            # Time Taken
            final_time = time.time()
            difference_time = final_time - begin_time
            difference_time_1 = round(difference_time, 2)
            create.create_text(200, 475, text = str(difference_time_1) + ' seconds', font=('Baskerville', 17))

    def call(event):
        global moves, prev_1
        i = event.x // 100
        j = event.y // 100
        if board[i][j] != '.':
            return
        moves += 1
        if (prev_1[0] > 4):
            prev_1[0] = i
            prev_1[1] = j
            board[i][j] = ans[i][j]
            quiz_board()
        else:
            board[i][j] = ans[i][j]
            quiz_board()
            if (ans[i][j] == board[prev_1[0]][prev_1[1]]):
                print("Pair Matched")
                prev_1 = [100, 100]
                quiz_board()
                return
            else:
                board[prev_1[0]][prev_1[1]] = '.'
                quiz_board()
                prev_1 = [i, j]
                return

    create.bind("<Button-1>", call)

    def exit_function1():
        window.destroy()
    exit_button = Button(window, text='EXIT', font=('Baskerville', 18), foreground='Red', command=exit_function1)
    exit_button.pack(side=BOTTOM)

    def return2homepage():
        create.destroy()
        return_button.destroy()
        exit_button.destroy()
        main_window()
    return_button = Button(window, text='RETURN', font=('Baskerville', 18), foreground='Red', command=return2homepage)
    return_button.pack(side=BOTTOM)

    quiz_board()
    mainloop()
# Level 1 Code Finished

# Level 2 Code
def medium_level():
    global begin_time
    begin_time = time.time()
    create = Canvas(width = 600, height = 700)
    create.pack()

    board = [list('.' * 6) for count in range(6)]
    ans = list('AABBCCDDEEFFGGHHIIJJKKLLMMNNOOPPQQRR')
    random.shuffle(ans)
    ans = [ans[:6],
           ans[6:12],
           ans[12:18],
           ans[18:24],
           ans[24:30],
           ans[30:]]

    def draw(x, y, z):
        if x == 'A':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Red', outline='Black')
        elif x == 'B':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Green', outline='Black')
        elif x == 'C':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Blue', outline='Black')
        elif x == 'D':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='Yellow', outline='Black')
        elif x == 'E':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='Brown', outline='Black')
        elif x == 'F':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='Orange', outline='Black')
        elif x == 'G':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20,
                                          100 * z + 100 - 20, fill='Purple', outline='Black')
        elif x == 'H':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20,
                                          100 * z + 100 - 20, fill='Pink', outline='Black')
        elif x == 'I':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20,
                                          100 * z + 100 - 20, fill='AliceBlue', outline='Black')
        elif x == 'J':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20,
                                          100 * z + 100 - 20, fill='Aqua', outline='Black')
        elif x == 'K':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20,
                                          100 * z + 100 - 20, fill='DarkSlateBlue', outline='Black')
        elif x == 'L':
            shape = create.create_polygon(100 * y + 50, z * 100 + 20, 100 * y + 20, 100 * z + 100 - 20,
                                          100 * y + 100 - 20,
                                          100 * z + 100 - 20, fill='Beige', outline='Black')
        elif x == 'M':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Chocolate', outline='Black')
        elif x == 'N':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='Chartreuse1', outline='Black')
        elif x == 'O':
            shape = create.create_rectangle(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                            fill='BlueViolet', outline='Black')
        elif x == 'P':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='DarkSalmon', outline='Black')
        elif x == 'Q':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='CadetBlue', outline='Black')
        elif x == 'R':
            shape = create.create_oval(100 * y + 20, z * 100 + 20, 100 * y + 100 - 20, 100 * z + 100 - 20,
                                       fill='Crimson', outline='Black')

    def quiz_board():
        global begin_time
        count = 0
        for i in range(6):
            for j in range(6):
                rec = create.create_rectangle(100 * i, j * 100, 100 * i + 100, 100 * j + 100, fill='Light Gray')
                if (board[i][j] != '.'):
                    draw(board[i][j], i, j)
                    count += 1
        if count >= 36:
            # moves
            create.create_text(300, 630, text = 'CONGRATULATIONS!!!\n You finished the game in:', font=('Baskerville', 17))
            create.create_text(300, 660, text = str(moves) + ' moves', font=('Baskerville', 17))
            # Time Taken
            final_time = time.time()
            difference_time = final_time - begin_time
            difference_time_1 = round(difference_time, 2)
            create.create_text(300, 680, text = str(difference_time_1) + ' seconds', font=('Baskerville', 17))

    def call(event):
        global moves, prev_1
        i = event.x // 100
        j = event.y // 100
        if board[i][j] != '.':
            return
        moves += 1
        if (prev_1[0] > 6):
            prev_1[0] = i
            prev_1[1] = j
            board[i][j] = ans[i][j]
            quiz_board()
        else:
            board[i][j] = ans[i][j]
            quiz_board()
            if (ans[i][j] == board[prev_1[0]][prev_1[1]]):
                print("Pair Matched")
                prev_1 = [100, 100]
                quiz_board()
                return
            else:
                board[prev_1[0]][prev_1[1]] = '.'
                quiz_board()
                prev_1 = [i, j]
                return

    create.bind("<Button-1>", call)

    def exit_function1():
        window.destroy()
    exit_button = Button(window, text='EXIT', font=('Baskerville', 18), foreground='Red', command=exit_function1)
    exit_button.pack(side=BOTTOM)

    def return2homepage():
        create.destroy()
        exit_button.destroy()
        return_button.destroy()
        main_window()
    return_button = Button(window, text='RETURN', font=('Baskerville', 18), foreground='Red', command=return2homepage)
    return_button.pack(side=BOTTOM)

    quiz_board()
    mainloop()
# Level 2 Code Finished

# Level 3 Code
def hard_level():
    global begin_time
    begin_time = time.time()
    create = Canvas(width = 660, height = 750)
    create.pack()

    board = [list('.' * 8) for count in range(8)]
    ans = list('AABBCCDDEEFFGGHHIIJJKKLLMMNNOOPPQQRRSSTTUUWWXXYYZZaabbccddeeffgg')
    random.shuffle(ans)
    ans = [ans[:8],
           ans[8:16],
           ans[16:24],
           ans[24:32],
           ans[32:40],
           ans[40:48],
           ans[48:56],
           ans[56:]]

    def draw(x, y, z):
        if x == 'A':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='Red', outline='Black')
        elif x == 'B':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='Green', outline='Black')
        elif x == 'C':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='Blue', outline='Black')
        elif x == 'D':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='Yellow', outline='Black')
        elif x == 'E':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='Brown', outline='Black')
        elif x == 'F':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='Orange', outline='Black')
        elif x == 'G':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='Purple', outline='Black')
        elif x == 'H':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='Pink', outline='Black')
        elif x == 'I':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='OliveDrab1', outline='Black')
        elif x == 'J':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='OliveDrab2', outline='Black')
        elif x == 'K':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='DarkSlateBlue', outline='Black')
        elif x == 'L':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='Beige', outline='Black')
        elif x == 'M':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='Chocolate', outline='Black')
        elif x == 'N':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='Chartreuse1', outline='Black')
        elif x == 'O':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='BlueViolet', outline='Black')
        elif x == 'P':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='DarkSalmon', outline='Black')
        elif x == 'Q':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='CadetBlue', outline='Black')
        elif x == 'R':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='Crimson', outline='Black')
        elif x == 'S':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='DarkGoldenRod', outline='Black')
        elif x == 'T':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='SeaGreen', outline='Black')
        elif x == 'U':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='DeepPink4', outline='Black')
        elif x == 'V':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='DeepPink1', outline='Black')
        elif x == 'W':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='DeepSkyBlue4', outline='Black')
        elif x == 'X':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='LightPink4', outline='Black')
        elif x == 'Y':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='Gold', outline='Black')
        elif x == 'Z':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='GoldenRod', outline='Black')
        elif x == 'a':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='Gold4', outline='Black')
        elif x == 'b':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='HotPink4', outline='Black')
        elif x == 'c':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='IndianRed', outline='Black')
        elif x == 'd':
            shape = create.create_rectangle(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                            fill='Khaki', outline='Black')
        elif x == 'e':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='Lavender', outline='Black')
        elif x == 'f':
            shape = create.create_polygon(80 * y + 50, z * 80 + 20, 80 * y + 20, 80 * z + 80 - 20, 80 * y + 80 - 20,
                                          80 * z + 80 - 20, fill='LavenderBlush4', outline='Black')
        elif x == 'g':
            shape = create.create_oval(80 * y + 20, z * 80 + 20, 80 * y + 80 - 20, 80 * z + 80 - 20,
                                       fill='LightBlue4', outline='Black')

    def quiz_board():
        global begin_time
        count = 0
        for i in range(8):
            for j in range(8):
                # rec = create.create_rectangle(100 * i, j * 100, 100 * i + 100, 100 * j + 100, fill= 'Light Gray')
                rec = create.create_rectangle(80 * i, j * 80, 80 * i + 80, 80 * j + 80, fill='Light Gray')
                if (board[i][j] != '.'):
                    draw(board[i][j], i, j)
                    count += 1
        if count >= 64:
            # moves
            create.create_text(325, 665, text = 'CONGRATULATIONS!!!\n You finished the game in:', font=('Baskerville', 17))
            create.create_text(325, 695, text = str(moves) + ' moves', font=('Baskerville', 17))
            # Time Taken
            final_time = time.time()
            difference_time = final_time - begin_time
            difference_time_1 = round(difference_time, 2)
            create.create_text(325, 715, text = str(difference_time_1) + ' seconds', font=('Baskerville', 17))

    def call(event):
        global moves, prev_2
        i = event.x // 80
        j = event.y // 80
        if board[i][j] != '.':
            return
        moves += 1
        if (prev_2[0] > 8):
            prev_2[0] = i
            prev_2[1] = j
            board[i][j] = ans[i][j]
            quiz_board()
        else:
            board[i][j] = ans[i][j]
            quiz_board()
            if (ans[i][j] == board[prev_2[0]][prev_2[1]]):
                print("Pair Matched")
                prev_2 = [100, 100]
                quiz_board()
                return
            else:
                board[prev_2[0]][prev_2[1]] = '.'
                quiz_board()
                prev_2 = [i, j]
                return

    create.bind("<Button-1>", call)

    def exit_function1():
        window.destroy()
    exit_button = Button(window, text='EXIT', font=('Baskerville', 18), foreground='Red', command=exit_function1)
    exit_button.pack(side=BOTTOM)

    def return2homepage():
        create.destroy()
        exit_button.destroy()
        return_button.destroy()
        main_window()
    return_button = Button(window, text='RETURN', font=('Baskerville', 18), foreground='Red', command=return2homepage)
    return_button.pack(side=BOTTOM)

    quiz_board()
    mainloop()
# Level 3 Code Finished


# Final Run Code
mainloop()
window.mainloop()
