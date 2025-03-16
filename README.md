# party-celebration
import time
import random
import pygame

# Initialize Pygame
pygame.init()

# Screen setup
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("🎉 Party Celebration! 🎊")

# Colors
BLACK = (0, 0, 0)
COLORS = [(255, 0, 0), (0, 255, 0), (0, 0, 255), (255, 255, 0), (255, 0, 255), (0, 255, 255)]

# Load party sound
pygame.mixer.init()
party_sound = pygame.mixer.Sound("party_horn.wav")  # Make sure you have a party sound file
party_sound.play(-1)  # Loop party sound

# Particle class for confetti
class Confetti:
    def __init__(self):
        self.x = random.randint(0, WIDTH)
        self.y = random.randint(0, HEIGHT)
        self.color = random.choice(COLORS)
        self.size = random.randint(5, 15)
        self.speed = random.uniform(1, 3)
    
    def fall(self):
        self.y += self.speed
        if self.y > HEIGHT:
            self.y = 0  # Reset confetti position to top

# Create confetti list
confetti_list = [Confetti() for _ in range(100)]

running = True
clock = pygame.time.Clock()
while running:
    screen.fill(BLACK)
    
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    # Draw confetti
    for confetti in confetti_list:
        pygame.draw.circle(screen, confetti.color, (confetti.x, int(confetti.y)), confetti.size)
        confetti.fall()
    
    # Update screen
    pygame.display.flip()
    clock.tick(30)

pygame.quit()
