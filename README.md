# Mini-project-AI-games

## Aim: 

The aim of this program is to create a side-scrolling shooter game where the player can move, shoot bullets, and eliminate enemies moving across the screen.


## ALGORITHM:
### 1. Initialize the Game:

Import the Pygame library and initialize it.
Set up the screen dimensions and create a display window.
Define colors and load basic assets (e.g., player, bullet, and enemy surfaces).

### 2.Define Player Properties:

Set initial position and movement speed for the player.
Create logic to handle the player's movement with keyboard inputs (e.g., UP and DOWN arrow keys).

### 3.Bullet Creation and Properties:

Create a surface for bullets with a specified size and color.
Implement logic to shoot bullets when the SPACE key is pressed.
Move bullets across the screen and remove them when they go off-screen.

### 4.Enemy Creation and Movement:

Randomly spawn enemies on the right side of the screen and move them left.
Remove enemies when they move off-screen or are hit by a bullet.

### 5.Collision Detection:

Check for collisions between bullets and enemies.
Remove both the bullet and the enemy upon collision.

### 6.Draw Game Elements:

Draw the player, bullets, and enemies on the screen each frame.
Refresh the screen to display the updated positions of all game elements.

### 7.Game Loop:

Continuously run the game loop while the running flag is True.
Handle user input and events (e.g., quitting the game).
Update the positions of the player, bullets, and enemies.
Perform collision detection.
Render all game elements and update the display.

### 8.Exit the Game:

Stop the game loop when the user closes the window.
Quit Pygame and exit the program.


## PROGRAM:

```python
import pygame
import random


pygame.init()


SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Side-Scrolling Shooter")


WHITE = (255, 255, 255)


player_img = pygame.Surface((50, 30))
player_img.fill((0, 128, 255))
enemy_img = pygame.Surface((40, 30))
enemy_img.fill((255, 0, 0))


bullet_img = pygame.Surface((20, 10))  # Increased size
bullet_img.fill((0, 0, 0))  # Changed color to black


player_x = 50
player_y = SCREEN_HEIGHT // 2
player_speed = 5

bullets = []
bullet_speed = 7


enemies = []
enemy_spawn_time = 30
enemy_speed = 3

clock = pygame.time.Clock()


running = True
while running:
    screen.fill(WHITE)

   
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_SPACE:
                # Shoot a bullet
                bullet_x = player_x + 50
                bullet_y = player_y + 15
                bullets.append([bullet_x, bullet_y])

   
    keys = pygame.key.get_pressed()
    if keys[pygame.K_UP] and player_y > 0:
        player_y -= player_speed
    if keys[pygame.K_DOWN] and player_y < SCREEN_HEIGHT - 30:
        player_y += player_speed


    for bullet in bullets:
        bullet[0] += bullet_speed
    bullets = [b for b in bullets if b[0] < SCREEN_WIDTH]

 
    for bullet in bullets:
        screen.blit(bullet_img, bullet)

 
    if random.randint(1, enemy_spawn_time) == 1:
        enemy_x = SCREEN_WIDTH
        enemy_y = random.randint(0, SCREEN_HEIGHT - 30)
        enemies.append([enemy_x, enemy_y])

    
    for enemy in enemies:
        enemy[0] -= enemy_speed
    enemies = [e for e in enemies if e[0] > -40]


    for enemy in enemies:
        screen.blit(enemy_img, enemy)

    
    for enemy in enemies:
        for bullet in bullets:
            if bullet[0] < enemy[0] + 40 and bullet[0] + 20 > enemy[0] and bullet[1] < enemy[1] + 30 and bullet[1] + 10 > enemy[1]:
                bullets.remove(bullet)
                enemies.remove(enemy)
                break

 
    screen.blit(player_img, (player_x, player_y))

   
    pygame.display.flip()
    clock.tick(30)

pygame.quit()

```
### RESULT:
Thus,  to create a side-scrolling shooter game where the player can move, shoot bullets, and eliminate enemies moving across the screen is successfully implemented.

