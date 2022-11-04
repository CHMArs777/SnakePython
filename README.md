# Подключение библиотек
import pygame
import time
from random import randint

# Инициализация библиотеки pygame
pygame.init()

# Объявление переменных для цвета
white = (100, 255, 255)
black = (0, 0, 0)
red = (255, 0, 0)

dis_width = 800
dis_height = 400

dis = pygame.display.set_mode((dis_width, dis_height))
pygame.display.set_caption('SnakePython ')

game_over = False
#  начальное положение
x1 = randint(10, dis_width)
y1 = randint (10, dis_height)

xapple = randint(10, dis_width)
yapple = randint (10, dis_height)

# Размер змейки
snake_block = 15
apple_block = 15

x1_change = 0
y1_change = 0

xapple_change = 0
yapple_change = 0

clock = pygame.time.Clock()
snake_speed = 30

font_style = pygame.font.SysFont(None, 50)


def message(msg, color):
    mesg = font_style.render(msg, True, color)
    dis.blit(mesg, [dis_width / 2, dis_height / 2])


while not game_over:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            game_over = True
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                x1_change = -snake_block
                y1_change = 0
            elif event.key == pygame.K_RIGHT:
                x1_change = snake_block
                y1_change = 0
            elif event.key == pygame.K_UP:
                y1_change = -snake_block
                x1_change = 0
            elif event.key == pygame.K_DOWN:
                y1_change = snake_block
                x1_change = 0
            elif event.key == pygame.K_SPACE:
                y1_change = 0
                x1_change = 0
    #  Условия Проигрыша
    if x1 > dis_width or x1 < 0 or y1 > dis_height or y1 < 0:
        game_over = True
    x1 += x1_change
    y1 += y1_change
    dis.fill(white)

    # Для добавления используем метод draw
    pygame.draw.rect(dis, black, [x1, y1, snake_block, snake_block])
    pygame.draw.circle(dis, (50, 150, 0), (xapple, yapple), 10)

    pygame.display.update()

    clock.tick(snake_speed)

message("You lost", red)
pygame.display.update()
time.sleep(2)

pygame.quit()
quit()
