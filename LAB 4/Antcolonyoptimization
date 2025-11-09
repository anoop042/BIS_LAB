import random
import math

def distance(city1, city2):
    return math.sqrt((city1[0] - city2[0])**2 + (city1[1] - city2[1])**2)

def initialize_pheromone(num_cities, tau0):
    return [[tau0 for _ in range(num_cities)] for _ in range(num_cities)]

def roulette_wheel_selection(probabilities):
    r = random.random()
    cumulative = 0.0
    for i, p in enumerate(probabilities):
        cumulative += p
        if r <= cumulative:
            return i
    return len(probabilities) - 1

def ant_colony_optimization(cities, alpha=1.0, beta=5.0, evaporation_rate=0.5, Q=100, num_ants=None, max_iterations=100):
    num_cities = len(cities)
    if num_ants is None:
        num_ants = num_cities

    tau0 = 1.0 / (num_cities * sum(distance(cities[i], cities[(i+1) % num_cities]) for i in range(num_cities)))
    pheromone = initialize_pheromone(num_cities, tau0)

    best_tour = None
    best_length = float('inf')

    for iteration in range(max_iterations):
        all_tours = []
        all_lengths = []

        for ant in range(num_ants):
            start_city = random.randint(0, num_cities - 1)
            visited = [False] * num_cities
            visited[start_city] = True
            tour = [start_city]
            current_city = start_city

            while len(tour) < num_cities:
                unvisited_cities = [c for c in range(num_cities) if not visited[c]]
                probabilities = []

                denom = 0
                for city_j in unvisited_cities:
                    tau_ij = pheromone[current_city][city_j] ** alpha
                    dist_ij = distance(cities[current_city], cities[city_j])
                    eta_ij = (1.0 / dist_ij) ** beta if dist_ij > 0 else 0
                    denom += tau_ij * eta_ij

                for city_j in unvisited_cities:
                    tau_ij = pheromone[current_city][city_j] ** alpha
                    dist_ij = distance(cities[current_city], cities[city_j])
                    eta_ij = (1.0 / dist_ij) ** beta if dist_ij > 0 else 0
                    p = (tau_ij * eta_ij) / denom if denom > 0 else 0
                    probabilities.append(p)

                next_city_index = roulette_wheel_selection(probabilities)
                next_city = unvisited_cities[next_city_index]

                tour.append(next_city)
                visited[next_city] = True
                current_city = next_city

            tour_length = 0
            for i in range(num_cities):
                city_i = tour[i]
                city_j = tour[(i + 1) % num_cities]
                tour_length += distance(cities[city_i], cities[city_j])

            all_tours.append(tour)
            all_lengths.append(tour_length)

            if tour_length < best_length:
                best_length = tour_length
                best_tour = tour

        for i in range(num_cities):
            for j in range(num_cities):
                pheromone[i][j] *= (1 - evaporation_rate)

        for tour, length in zip(all_tours, all_lengths):
            deposit_amount = Q / length
            for i in range(num_cities):
                city_i = tour[i]
                city_j = tour[(i + 1) % num_cities]
                pheromone[city_i][city_j] += deposit_amount
                pheromone[city_j][city_i] += deposit_amount

        print(f"Iteration {iteration + 1}/{max_iterations}, best length: {best_length:.4f}")

    return best_tour, best_length

cities = [
    (0, 0),
    (1, 5),
    (5, 2),
    (6, 6),
    (8, 3),
    (7, 8),
    (2, 7)
]

best_tour, best_length = ant_colony_optimization(cities, max_iterations=50)
print("Best tour:", best_tour)
print("Best tour length:", best_length)
