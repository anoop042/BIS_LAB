import numpy as np

def parallel_cellular_algorithm(f, grid_size, num_cells, max_iterations):
    grid = np.random.rand(num_cells, len(grid_size))
    fitness = np.array([f(cell) for cell in grid])
    for _ in range(max_iterations):
        new_grid = grid.copy()
        for i in range(num_cells):
            neighbors = grid[np.random.choice(num_cells, 3, replace=False)]
            best_neighbor = neighbors[np.argmax([f(n) for n in neighbors])]
            new_grid[i] = (grid[i] + best_neighbor) / 2
        grid = np.clip(new_grid, 0, 1)
        fitness = np.array([f(cell) for cell in grid])
    best_index = np.argmax(fitness)
    return grid[best_index], fitness[best_index]

def f(x):
    return -np.sum((x - 0.5)**2)

best_solution, best_fitness = parallel_cellular_algorithm(f, [1,1], 20, 50)
print(best_solution, best_fitness)
