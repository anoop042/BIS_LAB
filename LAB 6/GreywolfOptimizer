import numpy as np

def gwo(fitness_func, dim, bounds, num_wolves=20, max_iter=100):
    lb, ub = bounds
    wolves = np.random.uniform(lb, ub, (num_wolves, dim))
    fitness = np.array([fitness_func(w) for w in wolves])
    idx = np.argsort(fitness)
    alpha, beta, delta = wolves[idx[0]], wolves[idx[1]], wolves[idx[2]]

    for t in range(max_iter):
        a = 2 - 2 * (t / max_iter)
        for i in range(num_wolves):
            for j in range(dim):
                r1, r2 = np.random.rand(), np.random.rand()
                A1, C1 = 2 * a * r1 - a, 2 * r2
                D_alpha = abs(C1 * alpha[j] - wolves[i][j])
                X1 = alpha[j] - A1 * D_alpha

                r1, r2 = np.random.rand(), np.random.rand()
                A2, C2 = 2 * a * r1 - a, 2 * r2
                D_beta = abs(C2 * beta[j] - wolves[i][j])
                X2 = beta[j] - A2 * D_beta

                r1, r2 = np.random.rand(), np.random.rand()
                A3, C3 = 2 * a * r1 - a, 2 * r2
                D_delta = abs(C3 * delta[j] - wolves[i][j])
                X3 = delta[j] - A3 * D_delta

                wolves[i][j] = (X1 + X2 + X3) / 3
            wolves[i] = np.clip(wolves[i], lb, ub)

        fitness = np.array([fitness_func(w) for w in wolves])
        idx = np.argsort(fitness)
        alpha, beta, delta = wolves[idx[0]], wolves[idx[1]], wolves[idx[2]]

    return alpha, fitness_func(alpha)

def sphere(x):
    return np.sum(x**2)

best_solution, best_value = gwo(sphere, dim=5, bounds=(-10, 10), num_wolves=30, max_iter=100)
print("Best solution:", best_solution)
print("Best fitness value:", best_value)
