# Virtual-Machine-Based-Task-Scheduling-Using-G-PSO-Algorithm
G&amp;PSO algorithm improves the Virtual Machine Efficiency and Resource Utilization compared to traditional PSO algorithm
ABSTRACT

Virtualization technology has been widely used to virtualize single server into multiple servers, which not only creates an operating environment for a virtual machine-based cloud computing platform but also potentially improves its efficiency. Currently, most task scheduling-based algorithms used in cloud computing environments are slow to convergence or easily fall into a local optimum. This paper introduces a Greedy Particle Swarm Optimization (G&PSO) based algorithm to solve the task scheduling problem. It uses a greedy algorithm to quickly solve the initial particle value of a particle swarm optimization algorithm derived from a virtual machine-based cloud platform. The archived experimental results show that the algorithm exhibits better performance such as a faster convergence rate, stronger local and global search capabilities, and a more balanced workload on each virtual machine. Therefore, the G&PSO algorithm demonstrates improved virtual machine efficiency and resource utilization compared with the traditional particle swarm optimization algorithm

1	PROBLEM STATEMENT 
	
	Virtual Machine Based Task Scheduling Algorithm in a Cloud Computing 	Environment.

2	SYSTEM DESIGN

2.1 Proposed System Overview

	Population size (s) 
	Number of virtual machines (VM)
	Performance of virtual machines (MIPS)
	Number of tasks 
	Length range of task (MI)
	Inertial factor (W)
	Learning factor (c1)
	Learning factor (c2)
	Maximum number of iterations 


In this function, min i≤j≤M LoadVMSj  is the minimum time for all the virtual machines to complete all the tasks above, and max i≤j≤M LoadVMSj is the maximum time for all the virtual machines to complete all the tasks above. So the function is the ratio of the minimum load to the maximum load. The following conclusions can be drawn from Formula (3):
(1 )max i≤j≤M LoadVMSj  = 0 means the tasks do not yet start to schedule.
(2) Loadlevel = 0 and max i≤j≤M LoadVMSj  != 0 means there are idle virtual machines.
(3) Loadlevel = 1 means that the maximum load is equal to the minimum load, and that the load balanceis the best, i.e., the closer to 1, the better. 

     A fitness function is used to evaluate the merits of the particle positions. As the total task completion time is the key parameter for task-scheduling in cloud computing, the inverse of the total task completion time is used to represent the fitness function. The fitness function is defined as

      Fitness(i)=1/SFTi      1≤i≤s                

      SFT=max i ≤m ≤M(∑ kn=1 VM(m,n))        

      In Formula (4), SFTi represents the time needed to complete the task- scheduling for allocating the task at the i -th particle. 

     In Formula (5), SFT represents the time needed to complete all the tasks; VM(m, n) represents the time for the n-th task to run on the m-th virtual machine, and K is the number of tasks distributed to this virtual machine. Each iteration selects the particle with a larger fitness value, and one of these values is used as the globally optimal solution, which means that adopting this particle’ task allocation  scheme results in the shortest completion time.

The best position that the i -th particle has experienced is denoted as pbest =(pbesti1,pbesti2,…,pbestin). In the whole particle swarm, the best position that all particles have experienced is recorded as gbesti =(gbesti1,gbesti2,…,gbestin). In this formula, n represents the best location of the particle experience, in the range of the total number of tasks (1≤ n ≤T ).

        For each iteration, the value of the particle’s fitness function can be calculated using Formulas (4) and (5). The value of particle’s current fitness function is denoted as f(pi(t+1)):

      pbesti(t+1)=pbesti(t) , if f(pi(t+1) ≤f(pbesti(t))
                           pi(t+1), if (f(pi(t+1)> f(p(besti(t))                           
                           f(max(pbest(t))=getMax(f(pbesti(t)),
                           f(pbest2(t)),…,f(pbests(t)))                                
      gbest(t)=     max(pbest(t)),if f(max(pbest(t))>f(gbest);
                            gbest ,  else       
                                     
  2.2 Low-Level Design

   Step 1 Initialization of the particle swarm. The position and velocity of the particles are first initialized and the greedy algorithm is used to quickly obtain the initial solution Gov (i.e., a        feasible task allocation solution) and the expected total task completion time Gct; then, the best position gbest that the particles experience with Gov is initialized.
Greedy procedure: The procedure starts from index row 0 of the ETC matrix; it tries to allocate tasks to the virtual machine from the last column of each row in the ETC matrix. If the choice made is better than the others, then the assignment is finished; otherwise, the task is assigned to the virtual machine that makes the current result optimal. Moreover, if there are multiple allocation plans available, then the task is assigned to the virtual machine that has the least tasks, thus achieving simple load balancing.
Step 2 Calculate each particle’s fitness function value using Formulas (4) and (5).
Step 3 Update the optimal. Update the individual and group optimal based on Formulas (6)–(8):
(1) Compare the value of the particle’s fitness function to its individual optimal pbest, if the value of
the particle’s fitness function is better than pbest, then replace the value of pbest with the current position of the particle.
(2) Compare the particle’s fitness function value to its group optimal gbest, if the fitness function value of the particle is better than that of the initial solution calculated by the greedy algorithm, then reset the value of gbest with the particle’s current position.
Step 4 Update the speed and position of the particle using Formulas (9) and (10) respectively.
Step 5 Stop conditions. The loop will return to Step 2 until the stop conditions are met.


 

3   REQUIRED SPECIFICATION 

3.1 Architecture Specifications

The computer architecture and operating system of the cloud data center is x86 and Windows, respectively, where each virtual machine has a 1.2 GHz CPU, 2GB RAM, and 100GB hard drive, and all virtual machines were set to VMware..
	
3.2 Hardware Requirements     
   
1.2 GHz CPU, 
8GB RAM, and
1TB hard drive
	



3.3 Software Requirements

cloudsim-3.0.3.jar
cloudsim-3.0.3-sources.jar
cloudsim-examples-3.0.3.jar
cloudsim-examples-3.0.3-sources.jar
jswarm-pso_2_08
Netbeans 8.1
JDK












