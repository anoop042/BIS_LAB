import random
import math

class Particle:
    def __init__(self, dim, bounds):
        self.position = [random.uniform(bounds[0], bounds[1]) for _ in range(dim)]
        self.velocity = [random.uniform(-1, 1) for _ in range(dim)]
        self.personal_best_position = list(self.position)
        self.personal_best_fitness = float('inf')

def fitness_function(position):

    return sum(x**2 for x in position)

def vector_add(v1, v2):
    return [x + y for x, y in zip(v1, v2)]

def vector_subtract(v1, v2):
    return [x - y for x, y in zip(v1, v2)]

def vector_multiply_scalar(v, scalar):
    return [x * scalar for x in v]

def clamp(position, bounds):
    return [max(bounds[0], min(x, bounds[1])) for x in position]

def pso(num_particles, dim, bounds, max_iterations, inertia=0.5, cognitive_factor=1.5, social_factor=1.5):

    swarm = [Particle(dim, bounds) for _ in range(num_particles)]

    for particle in swarm:
        fitness = fitness_function(particle.position)
        particle.personal_best_fitness = fitness
        particle.personal_best_position = list(particle.position)

    global_best_particle = min(swarm, key=lambda p: p.personal_best_fitness)
    global_best_position = list(global_best_particle.personal_best_position)
    global_best_fitness = global_best_particle.personal_best_fitness

    for _ in range(max_iterations):
        for particle in swarm:
            r1, r2 = random.random(), random.random()

            cognitive_velocity = vector_multiply_scalar(
                vector_subtract(particle.personal_best_position, particle.position), cognitive_factor * r1)
            social_velocity = vector_multiply_scalar(
                vector_subtract(global_best_position, particle.position), social_factor * r2)

            particle.velocity = vector_add(
                vector_multiply_scalar(particle.velocity, inertia),
                vector_add(cognitive_velocity, social_velocity)
            )

            particle.position = vector_add(particle.position, particle.velocity)

            particle.position = clamp(particle.position, bounds)

            fitness = fitness_function(particle.position)

            if fitness < particle.personal_best_fitness:
                particle.personal_best_fitness = fitness
                particle.personal_best_position = list(particle.position)

                if fitness < global_best_fitness:
                    global_best_fitness = fitness
                    global_best_position = list(particle.position)

    return global_best_position, global_best_fitness

num_particles = 30
dim = 2
bounds = (-10, 10)
max_iterations = 100

best_position, best_fitness = pso(num_particles, dim, bounds, max_iterations)
print(f"Best position: {best_position}")
print(f"Best fitness: {best_fitness}")
