import csv
import os

# CSV file name
filename = "training_data.csv"

# Create CSV file automatically if it does not exist
if not os.path.exists(filename):
    data = [
        ["Size", "Color", "Shape", "Class"],
        ["Big", "Red", "Circle", "No"],
        ["Small", "Red", "Triangle", "No"],
        ["Small", "Red", "Circle", "Yes"],
        ["Big", "Blue", "Circle", "No"],
        ["Small", "Blue", "Circle", "Yes"]
    ]

    with open(filename, "w", newline="") as file:
        writer = csv.writer(file)
        writer.writerows(data)

# Read CSV file
with open(filename, "r") as file:
    reader = csv.reader(file)
    data = list(reader)

attributes = data[0][:-1]
examples = data[1:]

# Get all possible values of each attribute
values = []
for i in range(len(attributes)):
    values.append(set(row[i] for row in examples))

# Initial hypotheses
S = ["Ø"] * len(attributes)
G = [["?"] * len(attributes)]


# Check whether hypothesis covers an example
def covers(h, x):
    for i in range(len(x)):
        if h[i] != "?" and h[i] != x[i]:
            return False
    return True


# Check whether h1 is more general than h2
def more_general(h1, h2):
    for i in range(len(h1)):
        if h1[i] == "?":
            continue
        if h2[i] == "Ø":
            continue
        if h1[i] != h2[i]:
            return False
    return True


# Candidate Elimination Algorithm
for row in examples:

    x = row[:-1]
    target = row[-1]

    if target == "Yes":

        # Remove G hypotheses that do not cover positive example
        G = [g for g in G if covers(g, x)]

        # Generalize S
        if S == ["Ø"] * len(attributes):
            S = x.copy()
        else:
            for i in range(len(attributes)):
                if S[i] != x[i]:
                    S[i] = "?"

        # Remove G hypotheses that are less general than S
        G = [g for g in G if more_general(g, S)]

    else:

        new_G = []

        for g in G:

            if covers(g, x):

                # Specialize G
                for i in range(len(attributes)):

                    if g[i] == "?":

                        for value in values[i]:

                            if value != x[i]:

                                new_g = g.copy()
                                new_g[i] = value

                                # Must be more general than S
                                if more_general(new_g, S):
                                    new_G.append(new_g)

            else:
                new_G.append(g)

        G = new_G


# Display result
print("\nCandidate Elimination Algorithm")
print("--------------------------------")

print("\nSpecific Boundary (S):")
print(S)

print("\nGeneral Boundary (G):")
for g in G:
    print(g)

print("\nAll consistent hypotheses lie between S and G.")
