import pygame

pygame.init()

display_width = 800
display_height = 600

display = pygame.display.set_mode((display_width, display_height))

clock = pygame.time.Clock()


class Player:
    def __init__(self):
        self.starting_x = 100
        self.starting_y = 290
        self.player = pygame.Rect(self.starting_x, self.starting_y, 20, 20)
        self.x_vel = 0
        self.y_vel = 0

    def draw_player(self):
        pygame.draw.rect(display, "blue", self.player)

    def controls(self):
        keys_pressed = pygame.key.get_pressed()

        if keys_pressed[pygame.K_RIGHT]:
            self.x_vel = 3
        elif keys_pressed[pygame.K_LEFT]:
            self.x_vel = -3
        else:
            self.x_vel = 0

        if keys_pressed[pygame.K_UP]:
            self.y_vel = -3
        elif keys_pressed[pygame.K_DOWN]:
            self.y_vel = 3
        else:
            self.y_vel = 0

    def apply_movement(self):
        self.player.x += self.x_vel
        self.player.y += self.y_vel

    def collision_detection(self):
        # Horizontal Collision
        self.player.x += self.x_vel
        collided_wall_index = self.player.collidelist(walls.wall_list)
        if collided_wall_index >= 0:
            collided_wall = walls.wall_list[collided_wall_index]
            if self.x_vel > 0:
                self.player.right = collided_wall.left
                self.x_vel = 0
            elif self.x_vel < 0:
                self.player.left = collided_wall.right
                self.x_vel = 0
        self.player.x -= self.x_vel

        # Vertical Collision
        self.player.y += self.y_vel
        collided_wall_index = self.player.collidelist(walls.wall_list)
        if collided_wall_index >= 0:
            collided_wall = walls.wall_list[collided_wall_index]
            if self.y_vel > 0:
                self.player.bottom = collided_wall.top
                self.y_vel = 0
            elif self.y_vel < 0:
                self.player.top = collided_wall.bottom
                self.y_vel = 0
        self.player.y -= self.y_vel

    def update_player(self):
        self.controls()
        self.collision_detection()
        self.apply_movement()
        self.draw_player()


class Walls:
    def __init__(self):
        self.walls_data = [
            {"x": 0, "y": 0, "width": 800, "height": 20},
            {"x": 0, "y": 580, "width": 800, "height": 20},
            {"x": 0, "y": 0, "width": 20, "height": 800},
            {"x": 780, "y": 0, "width": 20, "height": 800},
            {"x": 650, "y": 240, "width": 20, "height": 200},
            {"x": 360, "y": 470, "width": 20, "height": 300},
            {"x": 500, "y": 0, "width": 20, "height": 150},
            {"x": 250, "y": 100, "width": 20, "height": 200},
            {"x": 400, "y": 300, "width": 100, "height": 20},
            {"x": 50, "y": 400, "width": 200, "height": 20},
            {"x": 0, "y": 100, "width": 150, "height": 20},
        ]
        self.wall_list = []
        for data in self.walls_data:
            self.wall_list.append(pygame.Rect(data["x"], data["y"], data["width"], data["height"]))

    def draw_walls(self):
        for wall in self.wall_list:
            pygame.draw.rect(display, "azure4", wall)


player = Player()
walls = Walls()

running = True

while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    display.fill("white")

    player.update_player()

    walls.draw_walls()

    pygame.display.flip()

    clock.tick(60)
