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

pygame.mixer.music.load('sounds/music.mp3') #загружаем саундтрек игры миксер чтобы звук накладывался друг на друга
pygame.mixer.music.set_volume(0.3) #громкость
pygame.mixer.music.play(-1) #бесконечное повторение музыки

sndFall = pygame.mixer.Sound('sounds/fall.wav') #даем название для воспроизведения

py, sy, ay = HEIGHT // 2, 0, 0  #положение птички, скорость, ускорение
player = pygame.Rect(WIDTH // 3, py, 34, 24) #рамки птички
frame = 0 #для анимации

state = 'start' #начальное полжение птичка прост стоит
timer = 10 #нельзя управлять в течение этого времени

pipes = [] #создаем список труб
bges = [] #для фона
pipesScores = []

pipeSpeed = 8 #скорость приближения труб
pipeGateSize = 200 #ширина дырки
pipeGatePos = HEIGHT // 2 #хз пока

bges.append(pygame.Rect(0, 0, 288, 600)) #рамка фон

lives = 5 #жизни
scores = 0 #начальное число очков

play = True #пока значение тру цикл
while play:
    for event in pygame.event.get():
        if event.type == pygame.QUIT: #если пользователь закрыл то кык
            play = False

    press = pygame.mouse.get_pressed() #придаем значение типа
    keys = pygame.key.get_pressed()
    click = press[0] or keys[pygame.K_SPACE] #два варика о тип левая кнопка мыши

    if timer: timer -= 1 #таймер стремится к нулю

    frame = (frame + 0.2) % 4 #смена крыльев
