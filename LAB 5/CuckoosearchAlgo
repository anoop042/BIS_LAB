import numpy as np

def f(x):
    return np.sum(x**2)

def levyflight(Lambda):
    u = np.random.randn() * 0.01
    v = np.random.randn()
    step = u / (abs(v)**(1/Lambda))
    return step

def cuckoosearch(n=20, dim=2, lb=-10, ub=10, pa=0.25, maxi=200):
    nests = np.random.uniform(lb, ub, (n, dim))
    fitness = np.array([f(x) for x in nests])
    for _ in range(maxi):
        cuckoo = nests[np.random.randint(n)] + levyflight(1.5) * np.random.randn(dim)
        cuckoo = np.clip(cuckoo, lb, ub)
        f_cuckoo = f(cuckoo)
        j = np.random.randint(n)
        if f_cuckoo < fitness[j]:
            nests[j] = cuckoo
            fitness[j] = f_cuckoo
        abandon = np.random.rand(n, dim) < pa
        steps = np.random.randn(n, dim) * (nests[np.random.permutation(n)] - nests)
        new_nests = nests + abandon * steps
        new_nests = np.clip(new_nests, lb, ub)
        new_fitness = np.array([f(x) for x in new_nests])
        for i in range(n):
            if new_fitness[i] < fitness[i]:
                nests[i] = new_nests[i]
                fitness[i] = new_fitness[i]
    best_idx = np.argmin(fitness)
    return nests[best_idx], fitness[best_idx]

best_cs, fit_cs = cuckoosearch()
print("Cuckoo Search Best Solution:", best_cs)
print("Fitness:", fit_cs)
