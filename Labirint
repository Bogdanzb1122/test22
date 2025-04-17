from pygame import *

mixer.init()
mixer.music.load('Beznaprag.mp3')
mixer.music.play(-1)  # -1 для бесконечного повторения
mixer.music.set_volume(0.1)

bonus_music = mixer.Sound('Bonuszvyk.wav')

# Класс-родитель для других спрайтов
class GameSprite(sprite.Sprite):
    def __init__(self, player_image, player_x, player_y, size_x, size_y):
        sprite.Sprite.__init__(self)
        self.image = transform.scale(image.load(player_image), (size_x, size_y))
        self.rect = self.image.get_rect()
        self.rect.x = player_x
        self.rect.y = player_y
    
    def reset(self):
        window.blit(self.image, (self.rect.x, self.rect.y))

# Класс главного игрока
class Player(GameSprite):
    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_x_speed, player_y_speed):
        GameSprite.__init__(self, player_image, player_x, player_y, size_x, size_y)
        self.x_speed = player_x_speed
        self.y_speed = player_y_speed
    
    def update(self):  
        if self.rect.x <= win_width-80 and self.x_speed > 0 or self.rect.x >= 0 and self.x_speed < 0:
            self.rect.x += self.x_speed
        platforms_touched = sprite.spritecollide(self, barriers, False)
        if self.x_speed > 0:
            for p in platforms_touched:
                self.rect.right = min(self.rect.right, p.rect.left)
        elif self.x_speed < 0:
            for p in platforms_touched:
                self.rect.left = max(self.rect.left, p.rect.right)
        if self.rect.y <= win_height-80 and self.y_speed > 0 or self.rect.y >= 0 and self.y_speed < 0:
            self.rect.y += self.y_speed
        platforms_touched = sprite.spritecollide(self, barriers, False)
        if self.y_speed > 0:
            for p in platforms_touched:
                if p.rect.top < self.rect.bottom:
                    self.rect.bottom = p.rect.top
        elif self.y_speed < 0:
            for p in platforms_touched:
                self.rect.top = max(self.rect.top, p.rect.bottom)

    def fire(self):
        bullet = Bullet('bulletik.png', self.rect.centerx, self.rect.top, 15, 20, 15)
        bullets.add(bullet)

# Класс спрайта-ворога
class Enemy_h(GameSprite):
    side = "left"
    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed, x1, x2):
        GameSprite.__init__(self, player_image, player_x, player_y, size_x, size_y)
        self.speed = player_speed
        self.x1 = x1
        self.x2 = x2

    def update(self):
        if self.rect.x <= self.x1: 
            self.side = "right"
        if self.rect.x >= self.x2:
            self.side = "left"
        if self.side == "left":
            self.rect.x -= self.speed
        else:
            self.rect.x += self.speed

class Enemy_v(GameSprite):
    side = "up"
    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed, y1, y2):
        GameSprite.__init__(self, player_image, player_x, player_y, size_x, size_y)
        self.speed = player_speed
        self.y1 = y1
        self.y2 = y2

    def update(self):
        if self.rect.y <= self.y1: 
            self.side = "down"
        if self.rect.y >= self.y2:
            self.side = "up"
        if self.side == "up":
            self.rect.y -= self.speed
        else:
            self.rect.y += self.speed

# Класс спрайта-кулі
class Bullet(GameSprite):
    def __init__(self, player_image, player_x, player_y, size_x, size_y, player_speed):
        GameSprite.__init__(self, player_image, player_x, player_y, size_x, size_y)
        self.speed = player_speed

    def update(self):
        self.rect.x += self.speed
        if self.rect.x > win_width + 10:
            self.kill()

# Создаем окно
win_width = 1100
win_height = 600
window = display.set_mode((win_width, win_height))
display.set_caption("Лабіринт")
back = transform.scale(image.load("Temless.jpg"), (win_width, win_height))

barriers = sprite.Group()
bullets = sprite.Group()
monsters = sprite.Group() 

# Создаем стены 
w1 = GameSprite('brickwall.png', 100, 500, 10, 110)
w2 = GameSprite('brickwall.png', 100, 500, 100, 10)
w3 = GameSprite('brickwall.png', 200, 400, 10, 110)
w4 = GameSprite('brickwall.png', 100, 400, 100, 10)
w5 = GameSprite('brickwall.png', 100, 300, 10, 110)
w6 = GameSprite('brickwall.png', 100, 300, 220, 10)
w7 = GameSprite('brickwall.png', 310, 300, 10, 200)
w8 = GameSprite('brickwall.png', 0, 130, 250, 12)
w9 = GameSprite('brickwall.png', 400, 0, 10, 140)
w10 = GameSprite('brickwall.png', 400, 70, 150, 10)
w11 = GameSprite('brickwall.png', 420, 290, 10, 310)
w12 = GameSprite('brickwall.png', 420, 290, 200, 13)
w13 = GameSprite('brickwall.png', 420, 450, 200, 13)
w14 = GameSprite('brickwall.png', 650, 0, 10, 110)
w15 = GameSprite('brickwall.png', 650, 100, 110, 10)
w16 = GameSprite('brickwall.png', 830, 100, 110, 10)
w17 = GameSprite('brickwall.png', 930, 0, 10, 210)
w18 = GameSprite('brickwall.png', 820, 450, 10, 150)
w19 = GameSprite('brickwall.png', 745, 450, 240, 10)
w20 = GameSprite('brickwall.png', 820, 290, 10, 160)
w21 = GameSprite('brickwall.png', 820, 290, 150, 10)

# Добавляем все стенки в группу
barriers.add(w1, w2, w3, w4, w5, w6, w7, w8, w9, w10, w11, w12, w13, w14, w15, w16, w17, w18, w19, w20, w21)

# Создаем спрайты
packman = Player('Piramid.png', 5, win_height - 80, 45, 40, 0, 0)
monster1 = Enemy_v('ghost.png', win_width - 70, 360, 40, 40, 7, 300, 560)
monster2 = Enemy_h('goblin.png', win_width - 270, 500, 40, 40, 6, 429, win_width - 319)
monster3 = Enemy_h('redmonster.png', 20, 50, 45, 45, 7, 0, 350)
monster4 = Enemy_v('Kavboy.png', 30, 300, 40, 40, 5, 200, 550)
monster5 = Enemy_h('Paychok.png', 656, 25, 45, 45, 4, 670, 890)
monster6 = Enemy_h('Squid.png', 400, 520, 40, 40, 3, 100, 380) 
monster7 = Enemy_v('orc.png', 660, 200, 55, 55, 16, 110, 410)

monsters.add(monster1, monster2, monster3, monster4, monster5, monster6, monster7)

bonus = sprite.Group()
bonus.add(GameSprite("bonusik.png", win_width - 222, win_height - 100, 45, 45))
bonus.add(GameSprite("bonusik.png", 50, 44, 45, 45))
bonus.add(GameSprite("bonusik.png", 130, 333, 45, 45))
bonus.add(GameSprite("bonusik.png", 470, 500, 45, 45))
bonus.add(GameSprite("bonusik.png", 777, 30, 40, 40))
bonus.add(GameSprite("bonusik.png", 450, 20, 38, 38))

# Круг победы
circle_x = win_width - 55 
circle_y = 40 
circle_radius = 30
circle_color = (127, 103, 224)

# Флаг для окончания игры
finish = False

# Игровой цикл
run = True
while run:
    time.delay(50)

    for e in event.get():
        if e.type == QUIT:
            run = False
        elif e.type == KEYDOWN:
            if e.key == K_a:
                packman.x_speed = -5
            elif e.key == K_d:
                packman.x_speed = 5
            elif e.key == K_w:
                packman.y_speed = -5
            elif e.key == K_s:
                packman.y_speed = 5
            elif e.key == K_SPACE:
                packman.fire()
        elif e.type == KEYUP:
            if e.key == K_a or e.key == K_d:
                packman.x_speed = 0
            elif e.key == K_w or e.key == K_s:
                packman.y_speed = 0

    if not finish:
        window.blit(back, (0, 0))

        # Обновляем спрайты
        packman.update()
        bullets.update()

        # Отображаем спрайты
        packman.reset()
        bullets.draw(window)
        barriers.draw(window)

        shotkill_sound = mixer.Sound('shotkill.wav')
        if sprite.groupcollide(monsters, bullets, True, True):
            shotkill_sound.play()
        monsters.update()
        monsters.draw(window)
        
        sprite.groupcollide(bullets, barriers, True, False)
        bonus.draw(window)
        
        if sprite.spritecollide(packman, bonus, True):
            
            bonus_music.play() 
        # круг победы в правом верхнем углу
        draw.circle(window, circle_color, (circle_x, circle_y), circle_radius)

        # Проверка коллизии с кругом
        if ((packman.rect.centerx - circle_x) ** 2 + (packman.rect.centery - circle_y) ** 2) < circle_radius ** 2:
            finish = True
            mixer.music.stop()
            mixer.music.load('pobedaa.mp3')
            mixer.music.play()
            # Надпись "You Win" по центру экрана
            win_rect = Rect(win_width // 2 - 100, win_height // 2 - 50, 200, 100)
            draw.rect(window, (128, 128, 128), win_rect)
            font.init()
            text = font.Font(None, 50).render("You Win!", True, (0, 255, 72))
            window.blit(text, (win_width // 2 - 80, win_height // 2 - 20))

        # Проверка на столкновение с монстрами
        if sprite.spritecollide(packman, monsters, False):
            finish = True
            mixer.music.stop()
            mixer.music.load('proigrall.mp3')
            mixer.music.play()
            game_over_image = image.load("gameOver.png")
            window.blit(game_over_image, (win_width // 2 - game_over_image.get_width() // 2, win_height // 2 - game_over_image.get_height() // 2))

    display.update()


