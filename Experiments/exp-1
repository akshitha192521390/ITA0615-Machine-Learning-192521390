data = [
    ["Sunny", "Warm", "Normal", "Strong", "Warm", "Same", "Yes"],
    ["Sunny", "Warm", "High",   "Strong", "Warm", "Same", "Yes"],
    ["Rainy", "Cold", "High",   "Strong", "Warm", "Change", "No"],
    ["Sunny", "Warm", "High",   "Strong", "Cool", "Change", "Yes"]
]


hypothesis = ["Ø", "Ø", "Ø", "Ø", "Ø", "Ø"]

for row in data:
    
    if row[-1] == "Yes":

        for i in range(len(hypothesis)):
            if hypothesis[i] == "Ø":
                hypothesis[i] = row[i]

            elif hypothesis[i] != row[i]:
                hypothesis[i] = "?"

print("Most Specific Hypothesis:")
print(hypothesis)
