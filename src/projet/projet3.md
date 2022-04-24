# Jeu 2048

Votre projet

## Codeplay

```{codeplay}
from turtle import *
from random import choice
from time import sleep
case_num = {(-290, 290): 0, (-140, 290) : 0, (10, 290) : 0, (160, 290) : 0, (-290, 140) : 0, (-140, 140) : 0,
            (10, 140) : 0, (160, 140) : 0, (-290, -10) : 0, (-140, -10) : 0, (10, -10) : 0, (160, -10) : 0,
            (-290, -160) : 0, (10, -160) : 0, (160, -160) : 0, (-140, -160) : 0, (310, 290): 'stop', (310, 140): 'stop',
            (310, -10): 'stop', (310, -160): 'stop', (-440, 290): 'stop',(-440, 140): 'stop', (-440, -10): 'stop',
            (-440, -160): 'stop', (-290, 440): 'stop', (-140, 440): 'stop',(10, 440): 'stop', (160, 440): 'stop',
            (-290, -310): 'stop', (-140, -310): 'stop', (10, -310): 'stop', (160, -310): 'stop'}
case_num_memory = case_num

color_num = {0 : 'darkgrey', 2 : 'whitesmoke', 4 : 'MistyRose' , 8 : 'plum1', 16 : 'orchid2', 32 : 'magenta',
             64 : 'magenta3', 128 : 'DeepPink', 256 : 'MediumVioletRed', 512 : 'VioletRed1', 1024 : 'LightSeaGreen',
             2048 : 'turquoise1'}
pause, modifi , nbr, score, endjeu = 0, 0, 0, 0, 1
hist = []
speed(0)
hideturtle()
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
            
    def __str__(self):
        return f'Case({self.pos}, {self.text})'

class Button:
    def __init__(self, pos, text, size, color= 'Lightgrey'):
        self.pos = pos
        self.size = size
        self.text = text
        self.color = color
        self.draw()

    def draw(self):
        goto(self.pos)
        fillcolor(self.color)
        begin_fill()
        for x in self.size * 2:
            forward(x)
            left(90)
        end_fill()
        x, y = self.pos
        w, h = self.size
        goto(x+w/2, y+h/4 - 5)
        color('black')
        write(self.text, font=('Arial', h//2), align='center')

    def __str__(self):
        return f'Button({self.pos}, {self.text})'

    def inside(self, p):
        x, y = self.pos
        w, h = self.size
        return 0 < p[0]-x < w and 0 < p[1]-y < h


def end(text):
    global endjeu
    endjeu == 1
    global hist
    color('aliceblue')
    goto(-400, -400)
    begin_fill()
    for pos in (315, -400), (315, 400), (-400, 400):
        goto(pos)
    end_fill()
    color('black')
    goto(0, 0)
    write(text, font=('Arial', 40), align='center')
    goto(0, -250)
    write('historique: ' + str(hist), font=('Arial', 12), align='center')
#et si trop grand?    


def historique(direction):
    global hist
    if direction == 'h':
        hist.append('↑')
    elif direction == 'b':
        hist.append('↓')
    elif direction == 'd':
        hist.append('→')
    elif direction == 'g':
        hist.append('←')
        

def résultat():
    global score
    global case_num
    goto(-300, -350)
    width(40)
    down()
    color('aliceblue')
    goto(300, -350)
    up()
    width(5)
    color('black')
    goto(0, -375)
    nbrmax1 = []
    for nbr in case_num:
        if case_num[nbr] != 'stop':
            nbrmax1.append(case_num[nbr])
    nbrmax = max(nbrmax1)
    write('score: ' + str(score) + 10 * ' ' + 'nombre max: ' + str(nbrmax), font=('Arial', 25), align='center')
    if nbrmax == 2048:
        end('2048 c\'est la win!')
#marche pas en cas de new
 
 
def new():
    sleep(0.2)
    global nbr
    listey = (290, 140, -10, -160)
    listex = (160, 10, -140, -290)
    x = choice(listex)
    y = choice(listey)
    global case_num
    if nbr == 17:
        end('Game Over')
    elif case_num[(x, y)] == 0 and case_num[(x, y)] != 'stop':
        Case2 = Case((x, y), 2)
        case_num[(x, y)] = 2
        nbr += 1
        global pause
        pause = 1
        global score
        score += 2
    else:
        new()
        
        
def changement(pos, suiv):
    global case_num
    if pos != suiv:
        if case_num[suiv] == 0:
            nbrsuiv = case_num[pos]
        else:
            nbrsuiv = case_num[pos] * 2
        Casei = Case(suiv, nbrsuiv)
        case_num[suiv] = nbrsuiv
        Case0 = Case(pos, 0)
        case_num[pos] = 0
        global nbr
        nbr -= 1
        global modifi
        modifi = 1
    
    
def opération(x, y, direction):
    if direction == 'h':
        return x, y + 150
    elif direction == 'b':
        return x, y - 150
    elif direction == 'd':
        return x + 150, y
    elif direction == 'g':
        return x - 150, y
    
    
def opération_inverse(x, y, direction):
    if direction == 'h':
        return x, y - 150
    elif direction == 'b':
        return x, y + 150
    elif direction == 'd':
        return x - 150, y
    elif direction == 'g':
        return x + 150, y


def notsame(pos, direction, suiv):
    global case_num
    fusible = 0
    while True:
        if case_num[suiv] == 0:
            x, y = suiv
            suiv = opération(x, y, direction)
            fusible += 1
            if fusible > 5:
                break
#bloquage du curseur sans raisons -> à résoudre
        elif case_num[suiv] == 'stop':
            x, y = suiv
            suiv = opération_inverse(x, y, direction)
            changement(pos, suiv)
            break
        elif case_num[pos] == case_num[suiv]:
            changement(pos, suiv)
            break
        elif case_num[pos] != case_num[suiv]:
            x, y = suiv
            suiv = opération_inverse(x, y, direction)
            changement(pos, suiv)
    
    
def calcul(pos, direction):
    global case_num
    x, y = pos
    suiv = opération(x, y, direction)
    if suiv in case_num:
        if case_num[suiv] == case_num[pos]:
            changement(pos, suiv)
        else:
            notsame(pos, direction, suiv)
                
                
def mouvement(direction):
    global endjeu
    if endjeu:
        global modifi
        modifi = 0
        global case_num
        for i in range(4):
            for pos in case_num:
                if case_num[pos] != 0 and case_num[pos] != 'stop':
                    calcul(pos, direction)
        if modifi == 1:         
            new()
            résultat()
        else:
            global pause
            pause = 1
        historique(direction)
   
   
def haut():
    global pause
    if pause == 1:
        pause = 0
        mouvement('h')
        
        
def bas():
    global pause
    if pause == 1:
        pause = 0
        mouvement('b')


def gauche():
    global pause
    if pause == 1:
        pause = 0
        mouvement('g')


def droite():
    global pause
    if pause == 1:
        pause = 0
        mouvement('d')


def main():
    dot(2000, 'aliceblue')
    tour()
    cases()
    new()
    résultat()
    
    
def newgame():
    global pause
    global modifi
    global nbr
    global score
    global endjeu
    global hist
    global case_num
    global case_num_memory
    pause, modifi , nbr, score, endjeu = 0, 0, 0, 0, 1
    case_num = case_num_memory
    hist = []
    tour()
    cases()
    new()
    résultat()
    
def f(x, y):
    if Button_end.inside((x, y)):
        end('Tant Pis')
    if Button_new.inside((x, y)):
        newgame()

main()
Button_end = Button((350, 100), 'Exit', (80, 30))
Button_new = Button((350, -100), 'New', (80, 30))
s = getscreen()
s.onkey(haut, 'Up')
s.onkey(bas, 'Down')
s.onkey(gauche, 'Left')
s.onkey(droite, 'Right')
s.onclick(f)
s.listen()


```

