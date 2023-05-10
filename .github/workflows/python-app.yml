from pulp import *

# Create the 'prob' variable to contain the problem data
prob = LpProblem("Warehouse Distribution", LpMinimize)

# Decision variables
warehouses = ['W1', 'W2', 'W3']
customers = ['C1', 'C2', 'C3', 'C4']

choices = LpVariable.dicts("Choice", (warehouses, customers), lowBound=0, cat='Integer')

# Objective Function
prob += lpSum([20*choices['W1']['C1'], 40*choices['W1']['C2'], 70*choices['W1']['C3'], 50*choices['W1']['C4'],
               100*choices['W2']['C1'], 60*choices['W2']['C2'], 90*choices['W2']['C3'], 80*choices['W2']['C4'],
               10*choices['W3']['C1'], 110*choices['W3']['C2'], 30*choices['W3']['C3'], 200*choices['W3']['C4']])

# Constraints
# Supply Constraints
prob += lpSum([choices['W1'][j] for j in customers]) <= 400
prob += lpSum([choices['W2'][j] for j in customers]) <= 1500
prob += lpSum([choices['W3'][j] for j in customers]) <= 900

# Demand Constraints
prob += lpSum([choices[i]['C1'] for i in warehouses]) >= 700
prob += lpSum([choices[i]['C2'] for i in warehouses]) >= 600
prob += lpSum([choices[i]['C3'] for i in warehouses]) >= 1000
prob += lpSum([choices[i]['C4'] for i in warehouses]) >= 500

# The problem data is written to an .lp file
prob.writeLP("WarehouseDistribution.lp")

# The problem is solved using PuLP's choice of Solver
prob.solve()

# The status of the solution is printed to the screen
print("Status:", LpStatus[prob.status])

# Each of the variables is printed with its resolved optimum value
for v in prob.variables():
    print(v.name, "=", v.varValue)

# The optimized objective function value (Total Cost) is printed to the screen
print("Total Cost = ", value(prob.objective))
