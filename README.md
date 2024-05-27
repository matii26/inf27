# inf27


import math
from collections import defaultdict

# Helper function to find prime factors
def prime_factors(n):
    i = 2
    factors = []
    while i * i <= n:
        while (n % i) == 0:
            factors.append(i)
            n //= i
        i += 1
    if n > 1:
        factors.append(n)
    return factors

# Read numbers from file
with open('liczby.txt') as f:
    numbers = [int(line.strip()) for line in f]

# Zadanie 4.1
def zadanie_4_1(numbers):
    count = 0
    first_matching = None
    for number in numbers:
        str_num = str(number)
        if str_num[0] == str_num[-1]:
            if first_matching is None:
                first_matching = number
            count += 1
    return count, first_matching

# Zadanie 4.2
def zadanie_4_2(numbers):
    max_factors = 0
    max_unique_factors = 0
    number_max_factors = None
    number_max_unique_factors = None
    
    for number in numbers:
        factors = prime_factors(number)
        unique_factors = set(factors)
        if len(factors) > max_factors:
            max_factors = len(factors)
            number_max_factors = number
        if len(unique_factors) > max_unique_factors:
            max_unique_factors = len(unique_factors)
            number_max_unique_factors = number
            
    return number_max_factors, max_factors, number_max_unique_factors, max_unique_factors

# Zadanie 4.3
def zadanie_4_3(numbers):
    def find_good_trojki(numbers):
        good_trojki = []
        for i in range(len(numbers)):
            for j in range(len(numbers)):
                for k in range(len(numbers)):
                    if i != j and j != k and i != k:
                        if numbers[j] % numbers[i] == 0 and numbers[k] % numbers[j] == 0:
                            good_trojki.append((numbers[i], numbers[j], numbers[k]))
        return good_trojki
    
    def find_good_piatki(numbers):
        good_piatki = []
        for a in range(len(numbers)):
            for b in range(len(numbers)):
                for c in range(len(numbers)):
                    for d in range(len(numbers)):
                        for e in range(len(numbers)):
                            if len(set([a, b, c, d, e])) == 5:
                                if numbers[b] % numbers[a] == 0 and numbers[c] % numbers[b] == 0 and numbers[d] % numbers[c] == 0 and numbers[e] % numbers[d] == 0:
                                    good_piatki.append((numbers[a], numbers[b], numbers[c], numbers[d], numbers[e]))
        return good_piatki
    
    good_trojki = find_good_trojki(numbers)
    good_piatki = find_good_piatki(numbers)
    
    # Save good trójki to file
    with open('trojki.txt', 'w') as f:
        for trojka in good_trojki:
            f.write(f"{trojka[0]} {trojka[1]} {trojka[2]}\n")
    
    return len(good_trojki), len(good_piatki)

# Perform calculations
count_4_1, first_matching_4_1 = zadanie_4_1(numbers)
number_max_factors, max_factors, number_max_unique_factors, max_unique_factors = zadanie_4_2(numbers)
count_good_trojki, count_good_piatki = zadanie_4_3(numbers)

# Write results to file
with open('wyniki4.txt', 'w') as f:
    f.write(f"4.1 {count_4_1} {first_matching_4_1}\n")
    f.write(f"4.2 {number_max_factors} {max_factors} {number_max_unique_factors} {max_unique_factors}\n")
    f.write(f"4.3 {count_good_trojki} {count_good_piatki}\n")
