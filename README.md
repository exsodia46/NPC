import pygame
import random
import math
LEFT = 0
RIGHT = 1
UP = 2
DOWN = 3

class npc:
    def __init__(self):
        self.xpos = 100
        self.ypos = 100
        self.direction = RIGHT
        self.isAlive = True

    def draw(self, screen):
        if self.isAlive == True:
            pygame.draw.circle(screen, (255, 200, 255), (self.xpos, self.ypos), 20)
    def move(self, map, ticker,px,py):
        # randomly wander:
        if ticker % 40 == 0:
            num = random.randrange(0, 4)
            if num == 0:
                self.direction = RIGHT
            elif num == 1:
                self.direction = LEFT
        
        if map[int((self.ypos) / 50)][int((self.xpos - 10) / 50)] == 2 :
            self.xpos+=3

        #right collision
        if map[int((self.ypos) / 50)][int((self.xpos +30 + 5) / 50)] == 2 :
            self.xpos-=3

        #up colision
        if map[int((self.ypos-10) / 50)][int((self.xpos) / 50)] == 2 :
            self.ypos+=3

        #down collision
        if map[int((self.ypos+35) / 50)][int((self.xpos) / 50)] == 2 :
            self.ypos-=3

        # check for collision and change direction if you've bumped
        if self.direction == RIGHT and map[int((self.ypos) / 50)][int((self.xpos + 20) / 50)] == 2:
            self.direction = UP
            self.xpos -= 6
        if self.direction == LEFT and map[int((self.ypos) / 50)][int((self.xpos - 20) / 50)] == 2:
            self.direction = DOWN
            self.xpos += 6

        if self.direction == LEFT and map[int((self.ypos) / 50)][int((self.xpos + 20) / 50)] == 2:
            self.direction = DOWN
            self.xpos += 6
        if self.direction == RIGHT and map[int((self.ypos) / 50)][int((self.xpos - 20) / 50)] == 2:
            self.direction = UP
            self.xpos -= 6

        if self.direction == RIGHT:
            self.xpos += 3
        elif self.direction == LEFT:
            self.xpos -= 3
        if self.direction == UP:
            self.xpos += 3
        elif self.direction == DOWN:
            self.xpos -= 3
