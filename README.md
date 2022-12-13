# SAU1
import pygame
from random import randint

pygame.init()

WIDTH, HEIGHT = 800, 600 #рамка игры
FPS = 60 #частота кадров

window = pygame.display.set_mode((WIDTH, HEIGHT)) #открыть рамку
clock = pygame.time.Clock() #ограничение по времени

pygame.display.set_caption('Flappy bird') #название игры в углу
pygame.display.set_icon(pygame.image.load('images/icon.png')) #иконка игры в углу

font1 = pygame.font.Font(None, 35) #размер шрифта жизни и очки

imgBG = pygame.image.load('images/background.png') #загружаем пикчи
imgBird = pygame.image.load('images/bird.png')
imgPT = pygame.image.load('images/pipe_top.png')
imgPB = pygame.image.load('images/pipe_bottom.png')
