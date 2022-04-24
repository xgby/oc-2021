# Jeu 2048

Votre projet

## Codeplay

```{codeplay}
from turtle import *
from random import choice
case_num = {(-290, 290): 0, (-140, 290) : 0, (10, 290) : 0, (160, 290) : 0, (-290, 140) : 0, (-140, 140) : 0,
            (10, 140) : 0, (160, 140) : 0, (-290, -10) : 0, (-140, -10) : 0, (10, -10) : 0, (160, -10) : 0,
            (-290, -160) : 0, (10, -160) : 0, (160, -160) : 0, (-140, -160) : 0, (310, 290): 'stop', (310, 140): 'stop',
            (310, -10): 'stop', (310, -160): 'stop', (-440, 290): 'stop',(-440, 140): 'stop', (-440, -10): 'stop',
            (-440, -160): 'stop', (-290, 440): 'stop', (-140, 440): 'stop',(10, 440): 'stop', (160, 440): 'stop',
            (-290, -310): 'stop', (-140, -310): 'stop', (10, -310): 'stop', (160, -310): 'stop'}
nbr = 0
color_num = {0 : 'darkgrey', 2 : 'whitesmoke', 4 : 'MistyRose' , 8 : 'plum1', 16 : 'orchid2', 32 : 'magenta',
             64 : 'magenta3', 128 : 'DeepPink', 256 : 'MediumVioletRed', 512 : 'VioletRed1', 1024 : 'LightSeaGreen',
             2048 : 'turquoise1'}
speed(0)
up()


def tour():
    color('grey')
    goto(-300, -310)
    begin_fill()
    for pos in (310, -310), (310, 300), (-300, 300):
        goto(pos)
    end_fill()
   
   
def cases():
    color('darkgrey')
    for y in 290, 140, -10, -160:
        goto(-290, y)
        for i in range(4):
            begin_fill()
            for i in range(4):
                forward(140)
                right(90)
            end_fill()
            forward(150)


class Case:
    def __init__(self, pos, text, size=(80, 30)):
        self.pos = pos
        self.size = size
        self.text = text
        self.draw()
        
    def draw(self):
        x, y = self.pos
        goto(x, y)
        global color_num
        couleur = color_num[self.text]
        color(couleur)
        begin_fill()
        for i in range(4):
            forward(140)
            right(90)
        end_fill()
        if self.text != 0:
            goto(x + 70, y - 80)
            w, h = self.size
            color('black')
            write(self.text, font=('Arial', h//2), align='center')
            
def new():
    global nbr
    listey = (290, 140, -10, -160)
    listex = (160, 10, -140, -290)
    x = choice(listex)
    y = choice(listey)
    global case_num
    if nbr == 17:
        goto(0, 0)
        dot(500, 'pink')
        write('Game Over', font=('Arial', 40), align='center')
    elif case_num[(x, y)] == 0 and case_num[(x, y)] != 'stop':
        Case2 = Case((x, y), 2)
        case_num[(x, y)] = 2
        nbr += 1
    else:
        new()
        
        
def changement(pos, suiv):
    global case_num
    if case_num[suiv] == 0:
        nbrsuiv = case_num[pos]
    else:
        nbrsuiv = case_num[pos] ** 2
    Casei = Case(suiv, nbrsuiv)
    case_num[suiv] = nbrsuiv
    Case0 = Case(pos, 0)
    case_num[pos] = 0
    global nbr
    nbr -= 1
    
    
def opération(x, y, direction):
    if direction == 'h':
        return x, y + 150
    elif direction == 'b':
        return x, y - 150
    elif direction == 'd':
        return x + 150, y
    elif direction == 'g':
        return x - 150, y

    
def possible(pos, direction):
    global case_num
    x, y = pos
    suiv = opération(x, y, direction)
    if suiv in case_num:
        if case_num[suiv] == case_num[pos]:
            changement(pos, suiv)
        else:
            while case_num[suiv] == 0 or case_num[suiv] == 'stop':
                if case_num[suiv] == 0:
                    x, y = suiv
                    suiv = opération(x, y, direction)
                elif case_num[suiv] == 'stop':
                    x, y = suiv
                    if direction == 'h':
                        suiv = (x, y - 150)
                    elif direction == 'b':
                        suiv = (x, y + 150)
                    elif direction == 'd':
                        suiv = (x - 150, y)
                    elif direction == 'g':
                        suiv = (x + 150, y)
                    changement(pos, suiv)
                    break

 
def mouvement(direction):
    global case_num
    for pos in case_num:
        if case_num[pos] != 0 and case_num[pos] != 'stop':
            possible(pos, direction)
    new()
   
def haut():
    mouvement('h')

def bas():
    mouvement('b')

def gauche():
    mouvement('g')
    
def droite():
    mouvement('d')
      
def base():
    tour()
    cases()
    new()
    
    
base()   
s = getscreen()
s.onkey(haut, 'Up')
s.onkey(bas, 'Down')
s.onkey(gauche, 'Left')
s.onkey(droite, 'Right')
s.listen()

```

