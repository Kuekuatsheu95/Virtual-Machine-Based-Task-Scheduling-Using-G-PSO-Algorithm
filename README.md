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

      Fitness(i)=1/SFTi      1≤i≤s                              ….(4)

      SFT=max i ≤m ≤M(∑ kn=1 VM(m,n))               ….(5)

      In Formula (4), SFTi represents the time needed to complete the task- scheduling for allocating the task at the i -th particle. 

     In Formula (5), SFT represents the time needed to complete all the tasks; VM(m, n) represents the time for the n-th task to run on the m-th virtual machine, and K is the number of tasks distributed to this virtual machine. Each iteration selects the particle with a larger fitness value, and one of these values is used as the globally optimal solution, which means that adopting this particle’ task allocation  scheme results in the shortest completion time.

The best position that the i -th particle has experienced is denoted as pbest =(pbesti1,pbesti2,…,pbestin). In the whole particle swarm, the best position that all particles have experienced is recorded as gbesti =(gbesti1,gbesti2,…,gbestin). In this formula, n represents the best location of the particle experience, in the range of the total number of tasks (1≤ n ≤T ).

        For each iteration, the value of the particle’s fitness function can be calculated using Formulas (4) and (5). The value of particle’s current fitness function is denoted as f(pi(t+1)):

      pbesti(t+1)=pbesti(t) , if f(pi(t+1) ≤f(pbesti(t))
                           pi(t+1), if (f(pi(t+1)> f(p(besti(t))                               ….(6)
                           f(max(pbest(t))=getMax(f(pbesti(t)),
                           f(pbest2(t)),…,f(pbests(t)))                                          ….(7)
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




























2.3 High-Level design
 

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

4   IMPLEMENTATION

4.1 SOURCE CODE

Constant.java
 /*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package FitnessFunction;

/**
 *
 * @author HP
 */
public class Constant {
    

public static final int NO_OF_TASKS = 100 ; // number of Cloudlets;

    public static  int NO_OF_DATA_CENTERS =10; // number of Datacenters;

    public static final int POPULATION_SIZE = 300; // Number of Particles.

}

PSO.java

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package FitnessFunction;

import net.sourceforge.jswarm_pso.Swarm;
import scheduler.SchedulerFitnessFunction;

/**
 *
 * @author HP
 */
public class PSO {
    
private static SchedulerParticle particles[];

    public static SchedulerFitnessFunction ff = new SchedulerFitnessFunction();

    private static Swarm swarm = new Swarm(Constant.POPULATION_SIZE, new SchedulerParticle(), ff);

    public PSO() 
    {

        initParticles();

    }





    public double[] run() {



        swarm.setMinPosition(0);

        swarm.setMaxPosition(Constant.NO_OF_DATA_CENTERS - 1);

        swarm.setMaxMinVelocity(0.5);

        swarm.setParticles(particles);

        swarm.setParticleUpdate(new SchedulerParticleUpdate(new SchedulerParticle()));



        for (int i = 0; i < 500; i++) {

            swarm.evolve();

            if (i % 10 == 0) {

                System.out.printf("Gloabl best at iteration (%d): %f\n", i, swarm.getBestFitness());

            }

        }



        System.out.println("\nThe best fitness value: " + swarm.getBestFitness() + " Best makespan: " + ff.calcMakespan(swarm.getBestParticle().getBestPosition()));

         

        System.out.println("The best solution is: ");

        SchedulerParticle bestParticle = (SchedulerParticle) swarm.getBestParticle();

        System.out.println(bestParticle.toString());

        

        return swarm.getBestPosition();

    }

    

    public void printBestFitness() {

    	System.out.println("\nThe best fitness value: " + swarm.getBestFitness() + " Best makespan: " + ff.calcMakespan(swarm.getBestParticle().getBestPosition()));

    }

    

    public double[][] getCommunTimeMatrix() { return ff.getCoumnTimeMatrix(); }

    

    public double[][] getExecTimeMatrix() { return ff.getExecTimeMatrix(); }

    

    private static void initParticles() {

        particles = new SchedulerParticle[Constant.POPULATION_SIZE];

        for (int i = 0; i < Constant.POPULATION_SIZE; ++i)

            particles[i] = new SchedulerParticle();

    }
}

SchedulerParticle.java

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package FitnessFunction;

/**
 *
 * @author HP
 */
import net.sourceforge.jswarm_pso.Particle;



import java.util.Random;



public class SchedulerParticle extends Particle {

    SchedulerParticle() {

        super(Constant.NO_OF_TASKS);

        double[] position = new double[Constant.NO_OF_TASKS];

        double[] velocity = new double[Constant.NO_OF_TASKS];



        for (int i = 0; i < Constant.NO_OF_TASKS; i++) {

            Random randObj = new Random();

            position[i] = randObj.nextInt(Constant.NO_OF_DATA_CENTERS);

            velocity[i] = Math.random();

        }

        setPosition(position);

        setVelocity(velocity);

    }

    

    @Override

    public String toString() {

        String output = "";

        for (int i = 0; i < Constant.NO_OF_DATA_CENTERS; i++) {

            String tasks = "";

            int no_of_tasks = 0;

            for (int j = 0; j < Constant.NO_OF_TASKS; j++) {

                if (i == (int) getPosition()[j]) {

                    tasks += (tasks.isEmpty() ? "" : " ") + j;

                    ++no_of_tasks;

                }

            }

            if (tasks.isEmpty()) output += "There is no tasks associated to Data Center " + i + "\n";

            else

                output += "There are " + no_of_tasks + " tasks associated to Data Center " + i + " and they are " + tasks + "\n";

        }

        return output;

    }

}
    

SchedulerParticleUpdate.java


/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package FitnessFunction;

/**
 *
 * @author HP
 */
import net.sourceforge.jswarm_pso.Particle;

import net.sourceforge.jswarm_pso.ParticleUpdate;

import net.sourceforge.jswarm_pso.Swarm;



public class SchedulerParticleUpdate extends ParticleUpdate {

    private static final double W = 0.9;

    private static final double C = 2.0;



    SchedulerParticleUpdate(Particle particle) {

        super(particle);

    }



    @Override

    public void update(Swarm swarm, Particle particle) {

        double[] v = particle.getVelocity();

        double[] x = particle.getPosition();

        double[] pbest = particle.getBestPosition();

        double[] gbest = swarm.getBestPosition();



        for (int i = 0; i < Constant.NO_OF_TASKS; ++i) {

            v[i] = W * v[i] + C * Math.random() * (pbest[i] - x[i]) + C * Math.random() * (gbest[i] - x[i]);

            x[i] = (int) (x[i] + v[i]);

        }

    }

}



SchedularFitnessFunction.java:


package org.pso.scheduler;

import net.sourceforge.jswarm_pso.FitnessFunction;

public class SchedulerFitnessFunction extends FitnessFunction {
    private static double[][] execTimeMatrix, communTimeMatrix;

    SchedulerFitnessFunction() {
        super(false);
        initMatrices();
    }

    @Override
    public double evaluate(double[] position) {
//        double alpha = 0.3;
//        return alpha * calcTotalTime(position) + (1 - alpha) * calcMakespan(position);
        return calcMakespan(position);
    }

    private double calcTotalTime(double[] position) {
        double totalCost = 0;
        for (int i = 0; i < Constants.NO_OF_TASKS; i++) {
            int dcId = (int) position[i];
            totalCost += execTimeMatrix[i][dcId] + communTimeMatrix[i][dcId];
        }
        return totalCost;
    }

    public double calcMakespan(double[] position) {
        double makespan = 0;
        double[] dcWorkingTime = new double[Constants.NO_OF_DATA_CENTERS];

        for (int i = 0; i < Constants.NO_OF_TASKS; i++) {
            int dcId = (int) position[i];
            if(dcWorkingTime[dcId] != 0) --dcWorkingTime[dcId];
            dcWorkingTime[dcId] += execTimeMatrix[i][dcId] + communTimeMatrix[i][dcId];
            makespan = Math.max(makespan, dcWorkingTime[dcId]);
        }
        return makespan;
    }
    public double[][] getExecTimeMatrix()  { return execTimeMatrix; }
    public double[][] getCoumnTimeMatrix() { return communTimeMatrix; }
    
    private void initMatrices() {
        System.out.println("Initializing input matrices (e.g. exec time & communication time matrices");
        execTimeMatrix = new double[Constants.NO_OF_TASKS][Constants.NO_OF_DATA_CENTERS];
        communTimeMatrix = new double[Constants.NO_OF_TASKS][Constants.NO_OF_DATA_CENTERS];

        for (int i = 0; i < Constants.NO_OF_TASKS; i++) {
            for (int j = 0; j < Constants.NO_OF_DATA_CENTERS; j++) {
                execTimeMatrix[i][j] = Math.random() * 500;
                communTimeMatrix[i][j] = Math.random() * 500 + 20;
            }
        }
    }
}




pso.java


package pso;
import com.sun.org.apache.bcel.internal.Constants;
import java.text.DecimalFormat;
import java.util.ArrayList;
import java.util.Calendar;
import java.util.HashMap;
import java.util.HashSet;
import java.util.Iterator;
import java.util.LinkedList;
import java.util.List;
import org.cloudbus.cloudsim.Cloudlet;
import org.cloudbus.cloudsim.CloudletSchedulerSpaceShared;
import org.cloudbus.cloudsim.Datacenter;
import org.cloudbus.cloudsim.DatacenterBroker;
import org.cloudbus.cloudsim.DatacenterCharacteristics;
import org.cloudbus.cloudsim.Host;
import org.cloudbus.cloudsim.Log;
import org.cloudbus.cloudsim.Pe;
import org.cloudbus.cloudsim.Storage;
import org.cloudbus.cloudsim.UtilizationModel;
import org.cloudbus.cloudsim.UtilizationModelFull;
import org.cloudbus.cloudsim.Vm;
import org.cloudbus.cloudsim.VmAllocationPolicySimple;
import org.cloudbus.cloudsim.VmSchedulerSpaceShared;
import org.cloudbus.cloudsim.core.CloudSim;
import org.cloudbus.cloudsim.provisioners.BwProvisionerSimple;
import org.cloudbus.cloudsim.provisioners.PeProvisionerSimple;
import org.cloudbus.cloudsim.provisioners.RamProvisionerSimple;
import scheduler.*;
import FitnessFunction.Constant;
import FitnessFunction.PSO;
import FitnessFunction.SchedulerParticle;
import FitnessFunction.SchedulerParticleUpdate;
public class pso {
static Datacenter[] datacenter;
private static List<Vm> vmlist;
private static List<Cloudlet> cloudletList;
private static final PSO PSOSchedularInstance = new PSO();;
public static double mapping[] = PSOSchedularInstance.run();
public double[] getPsoMapping() { return mapping; }
public static void main(String[] args) {
double execTimeMatrix[][] = PSOSchedularInstance.getExecTimeMatrix();
double communTimeMatrix[][] = PSOSchedularInstance.getCommunTimeMatrix();
Log.printLine("Starting Task Schedular Simulation...");
try {
	int num_user = 1;
	Calendar calendar = Calendar.getInstance();
	boolean trace_flag = false;
	CloudSim.init(num_user, calendar, trace_flag);
	datacenter = new Datacenter[Constant.NO_OF_DATA_CENTERS];
	for(int i = 0; i < Constant.NO_OF_DATA_CENTERS; i++) {
		datacenter[i] = createDatacenter("Datacenter_" + i);
}
	DatacenterBroker broker = createBroker();
	int brokerId = broker.getId;
	vmlist = new ArrayList<Vm>();        	
	int mips = 1000;
	long size = 10000;        	
	int ram = 512;
	long bw = 1000;
	int pesNumber = 1;
	String vmm = "Xen";
	for(int i = 0; i < Constant.NO_OF_DATA_CENTERS ; i++) {
	vmlist.add(new Vm(datacenter[i].getId(), brokerId, mips, pesNumber, ram, bw, size, vmm, new CloudletSchedulerSpaceShared()));
	}
broker.submitVmList(vmlist);
cloudletList = new ArrayList<Cloudlet>();
pesNumber = 1;
long fileSize = 300;
long outputSize = 300;
UtilizationModel utilizationModel = new UtilizationModelFull();
for(int i = 0; i < Constant.NO_OF_TASKS; i++) {
	Cloudlet cloudlet1 = new Cloudlet(i,  (int) (1e3 * (execTimeMatrix[i][(int) mapping[i]] + communTimeMatrix[i][(int) mapping[i]])), pesNumber, fileSize, outputSize, utilizationModel, utilizationModel, utilizationModel);
cloudlet1.setUserId(brokerId);
cloudletList.add(cloudlet1);
}
HashSet<Integer> dcIds = new HashSet<>();
HashMap<Integer, Integer> hm = new HashMap<>();
for(Datacenter dc: datacenter) {
	if(!dcIds.contains(dc.getId())) 
	dcIds.add(dc.getId());
}
Iterator<Integer> it = dcIds.iterator();
for(int i = 0; i < mapping.length; i++) {
	if(hm.containsKey((int) mapping[i])) continue;
	hm.put((int) mapping[i], (int) it.next());
}
for(int i = 0; i < mapping.length; i++) 
	mapping[i] = hm.containsKey((int) mapping[i]) ? hm.get((int) mapping[i]) : mapping[i];
//broker.submitMapping(mapping);
broker.submitCloudletList(cloudletList);
CloudSim.startSimulation();
List<Cloudlet> newList = broker.getCloudletReceivedList();
CloudSim.stopSimulation();
printCloudletList(newList);
Log.printLine("simulating PSO finished!");
}catch(Exception e) {
System.out.println("An error has been occurred!\n" + e.getMessage());
}
}
private static void printCloudletList(List<Cloudlet> list) {
int size = list.size();
Cloudlet cloudlet;
String indent = "    ";
Log.printLine();
Log.printLine("========== OUTPUT ==========");
Log.printLine("Cloudlet ID" + indent + "STATUS" + indent +
"Data center ID" + indent + "VM ID" + indent + "Time" + indent + "Start Time" + indent + "Finish Time");
double mxFinishTime = 0;
DecimalFormat dft = new DecimalFormat("###.##");
for (int i = 0; i < size; i++) {
cloudlet = list.get(i);
Log.print(indent + cloudlet.getCloudletId() + indent + indent);
if (cloudlet.getCloudletStatus() == Cloudlet.SUCCESS){
Log.print("SUCCESS");
Log.printLine( indent + indent + cloudlet.getResourceId() + indent + indent + indent + cloudlet.getVmId() +
indent + indent + dft.format(cloudlet.getActualCPUTime()) + indent + indent + dft.format(cloudlet.getExecStartTime())+
indent + indent + dft.format(cloudlet.getFinishTime()));
mxFinishTime = Math.max(mxFinishTime, cloudlet.getFinishTime());
}
}
PSOSchedularInstance.printBestFitness();
System.out.println(mxFinishTime);
}
private static Datacenter createDatacenter(String name){
List<Host> hostList = new ArrayList<Host>();
// In this example, it will have only one core.
List<Pe> peList = new ArrayList<Pe>();
int mips = 1000;
// 3. Create PEs and add these into a list.
peList.add(new Pe(0, new PeProvisionerSimple(mips))); // need to store Pe id and MIPS Rating
//4. Create Host with its id and list of PEs and add them to the list of machines
int hostId = 0;
int ram = 2048; //host memory (MB)
long storage = 1000000; //host storage
int bw = 10000;
//in this example, the VMAllocatonPolicy in use is SpaceShared. It means that only one VM
//is allowed to run on each Pe. As each Host has only one Pe, only one VM can run on each Host.
hostList.add(new Host(hostId,new RamProvisionerSimple(ram),new BwProvisionerSimple(bw), storage,  peList, new VmSchedulerSpaceShared(peList)
)); // This is our first machine
// 5. Create a DatacenterCharacteristics object that stores the
//    properties of a data center: architecture, OS, list of
//    Machines, allocation policy: time- or space-shared, time zone
//    and its price (G$/Pe time unit).
String arch = "x86";      // system architecture
String os = "Linux";          // operating system
String vmm = "Xen";
double time_zone = 10.0;         // time zone this resource located
double cost = 3.0;              // the cost of using processing in this resource
double costPerMem = 0.05;		// the cost of using memory in this resource
double costPerStorage = 0.001;	// the cost of using storage in this resource
double costPerBw = 0.0;			// the cost of using bw in this resource
LinkedList<Storage> storageList = new LinkedList<Storage>();	//we are not adding SAN devices by now
DatacenterCharacteristics characteristics = new DatacenterCharacteristics(
arch, os, vmm, hostList, time_zone, cost, costPerMem, costPerStorage, costPerBw);

// 6. Finally, we need to create a PowerDatacenter object.
Datacenter datacenter = null;
try {
datacenter = new Datacenter(name, characteristics, new VmAllocationPolicySimple(hostList), storageList, 0);
}
 catch (Exception e) {
e.printStackTrace();
}
return datacenter;
}
private static DatacenterBroker createBroker() {
DatacenterBroker broker = null;
try {
broker = new DatacenterBroker("Broker");
} catch (Exception e) {
e.printStackTrace();
}
return broker;
}
}












