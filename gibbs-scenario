import matplotlib.pyplot as plt
import random
print("Gibbs Sampling")

# Set node for initial run
node_a = random.randint(0, 1)
node_b = 1  # fixed
node_c = random.randint(0, 1)
node_d = random.randint(0, 1)

# Initialize counting variables
# total_runs_N = 300000
total_runs_N = 5000000
count_a = 0
list_of_a = []


# Set up the factors (constant)
factor_DA = [100, 1, 1, 100]
factor_AB = [30, 5, 1, 10]
factor_BC = [100, 1, 1, 100]
factor_CD = [1, 100, 100, 1]

nodes = [node_a, node_b, node_c, node_d]

# Loop through
for i in range(0, total_runs_N):
   # print("**** Starting the Loop ****")

   # Choose node to sample on
   sample_on = random.randint(0, 3)
   # sample_on = 2  # for testing

   # Make sure not to sample on the fixed variable(s)
   while sample_on == 1:
       sample_on = random.randint(0, 3)

   # Initialize the two subsets of factors to be joined
   reduced_factor_1 = [0, 0]
   reduced_factor_2 = [0, 0]

   # Case: Sample on A
   # print(nodes)

   node_a = nodes[0]
   node_b = nodes[1]
   node_c = nodes[2]
   node_d = nodes[3]

   if sample_on == 0:
       # print("Sampling on A")
       if node_d == 0:
           reduced_factor_1 = [factor_DA[0], factor_DA[1]]
       else:
           reduced_factor_1 = [factor_DA[2], factor_DA[3]]

       if node_b == 0:
           print("should never happen!")
           reduced_factor_2 = [factor_AB[0], factor_AB[2]]
       else:
           reduced_factor_2 = [factor_AB[1], factor_AB[3]]

   # Case: Sample on B
   elif sample_on == 1:
       print("Should not happen!!!")

   # Case: Sample on C
   elif sample_on == 2:
       # print("Sampling on C")
       if node_d == 0:
           reduced_factor_1 = [factor_CD[0], factor_CD[2]]
       else:
           reduced_factor_1 = [factor_CD[1], factor_CD[3]]

       if node_b == 0:
           print("SHOULD NEVER GET HERE")
           reduced_factor_2 = [factor_BC[0], factor_BC[1]]
       else:
           reduced_factor_2 = [factor_BC[2], factor_BC[3]]

   # Case: Sample on D
   elif sample_on == 3:
       # print("Sampling on D")
       if node_a == 0:
           reduced_factor_1 = [factor_DA[0], factor_DA[2]]
       else:
           reduced_factor_1 = [factor_DA[1], factor_DA[3]]

       if node_c == 0:
           reduced_factor_2 = [factor_CD[0], factor_CD[1]]
       else:
           reduced_factor_2 = [factor_CD[2], factor_CD[3]]

   # Join
   # print(reduced_factor_1)
   # print(reduced_factor_2)
   false_value = float(reduced_factor_1[0] * reduced_factor_2[0])
   true_value = float(reduced_factor_1[1] * reduced_factor_2[1])
   # print("false_value = " + str(false_value))
   # print("true_value = " + str(true_value))

   # Normalize
   new_probability = true_value / (true_value + false_value)
   # print(new_probability)

   # Sample from new probability (from number line)
   random_sample = random.uniform(0, 1)
   # print("random sample: " + str(random_sample))
   sample_result = 0
   if random_sample <= new_probability:
       # Sample result is a 1
       sample_result = 1
   # print("Sample Result = " + str(sample_result))

   # Replace nodes with newest sample (use indexing..)
   if sample_on == 0:
       nodes = [sample_result, node_b, node_c, node_d]
   if sample_on == 1:
       nodes = [node_a, sample_result, node_c, node_d]
   if sample_on == 2:
       nodes = [node_a, node_b, sample_result, node_d]
   if sample_on == 3:
       nodes = [node_a, node_b, node_c, sample_result]

   # Increment count_a
   if nodes[0] == 1:
       count_a = count_a + 1

   # print("i = " + str(i+1))
   probability_of_a = float(count_a / (i+1))
   list_of_a.append(probability_of_a)
   # print(nodes)

# print(list_of_a)
print("count_a = " + str(count_a))

print("new P value = " + str(probability_of_a))
print(float(count_a / total_runs_N))

axes = plt.gca()
axes.set_ylim([0, 1.0])
axes.set_ylabel("P(A|+b)")
axes.set_xlabel("N samples")
plt.title("P(A|+b) using Gibbs Sampling")
plt.xscale("log")
plt.plot(list_of_a)
# plt.plot(0.052)
plt.axhline(0.05658953769, color="red")
plt.show()

