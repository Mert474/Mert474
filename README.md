import pygame
import sys
import random

# Oyun başlangıcı
pygame.init()

# Ekran ayarları
WIDTH, HEIGHT = 800, 400
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Dinozor Oyunu")

# Renkler
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Dinozor özellikleri
dino_width, dino_height = 50, 50
dino_x = 50
dino_y = HEIGHT - dino_height - 10
dino_speed = 5

# Zemin özellikleri
ground_y = HEIGHT - 10
ground_color = (150, 150, 150)

# Cactus özellikleri
cactus_width, cactus_height = 30, 50
cactus_speed = 5
cactus_list = []

# FPS kontrol
clock = pygame.time.Clock()

# Oyun döngüsü
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    keys = pygame.key.get_pressed()
    if keys[pygame.K_SPACE]:
        # Dinozor zıplama işlemi
        pass

    # Dinozor hareketi
    dino_x += dino_speed

    # Cactus oluşturma
    if random.randint(0, 100) < 5:
        cactus_list.append([WIDTH, ground_y - cactus_height])

    # Cactus hareketi
    for cactus in cactus_list:
        cactus[0] -= cactus_speed

    # Cactus ekran dışına çıktığında silme
    cactus_list = [cactus for cactus in cactus_list if cactus[0] > 0]

    # Ekran temizleme
    screen.fill(WHITE)

    # Zemin çizimi
    pygame.draw.rect(screen, ground_color, (0, ground_y, WIDTH, 10))

    # Dinozor çizimi
    pygame.draw.rect(screen, BLACK, (dino_x, dino_y, dino_width, dino_height))

    # Cactus çizimi
    for cactus in cactus_list:
        pygame.draw.rect(screen, BLACK, (cactus[0], cactus[1], cactus_width, cactus_height))

    # Ekran güncelleme
    pygame.display.flip()

    # FPS ayarı
    clock.tick(30)
