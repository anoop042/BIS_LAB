import random

def objective_function(x):
    return x * x

def gene_expression(gene):
    return gene

def selection(population, fitness_list, minimize=True):
    sorted_pairs = sorted(zip(population, fitness_list), key=lambda x: x[1], reverse=not minimize)
    return [p for p, _ in sorted_pairs[:len(population)//2]]

def crossover(g1, g2):
    point = random.random()
    o1 = point * g1 + (1 - point) * g2
    o2 = point * g2 + (1 - point) * g1
    return o1, o2

def mutate(g, rate):
    if random.random() < rate:
        g += random.uniform(-1, 1)
    return g

def genetic_algorithm(N, m, c, g):
    population = [random.uniform(-10, 10) for _ in range(N)]
    best_solution = None
    best_fitness = float('inf')
    for _ in range(g):
        fitness_list = []
        for individual in population:
            phenotype = gene_expression(individual)
            fitness = objective_function(phenotype)
            fitness_list.append(fitness)
            if fitness < best_fitness:
                best_fitness = fitness
                best_solution = phenotype
        selected_parents = selection(population, fitness_list, True)
        new_population = []
        while len(new_population) < N:
            p1, p2 = random.sample(selected_parents, 2)
            if random.random() < c:
                o1, o2 = crossover(p1, p2)
            else:
                o1, o2 = p1, p2
            o1 = mutate(o1, m)
            o2 = mutate(o2, m)
            new_population.append(o1)
            if len(new_population) < N:
                new_population.append(o2)
        population = new_population
    return best_solution, best_fitness

best_solution, best_fitness = genetic_algorithm(N=20, m=0.1, c=0.8, g=50)
print(best_solution, best_fitness)
