Download Link: https://assignmentchef.com/product/solved-cse225-project3-binomial-heaps-to-implement-a-priority-queue
<br>
In this project, you are to use binomial heaps to implement a priority queue in a preemptive scheduling system.  A preemptive scheduling mechanism, shown in Fig. 1, operates as follows:

Processes bound to run are put in a priority queue (in this project a binomial heap (BH)) by a priority mechanism (in this project a function <em>f </em>(<em>e</em><em><sub>i </sub></em>,<em>t</em><em><sub>arr </sub></em>(<em>i</em>)) of the execution time, <em>e<sub>i</sub></em>, and arrival time, <em>t<sub>arr</sub>(i)</em>, of the process). Whenever the processor (P) is available, it is allocated for the process with the highest priority waiting in BH to run.  Any running process can use P only for a limited span of time called a <em>time slice</em> or <em>quantum</em>, <em>q</em>. If the current process runs to completion within <em>q</em>, then the next process with the highest priority waiting in BH attains the right to use P.  Otherwise (i.e., if the process is not finished), it is <em>preempted</em> (i.e., it releases P, its status saved for the next use of P and P is allocated to the next highest priority process in BH).  This switch of the right of use of P from one process to another is known as “context switching.”  The process that is preempted, is reenqueued, after its new priority is calculated based on its new arrival time so as to reallocate P later and run to completion.  This flow of events iterates until there are no more processes left in BH waiting for P.

<strong><em> </em></strong>

Figure. 1: Preemptive scheduling with a binomial queue                                  <strong><em> </em></strong>

<strong><em> </em></strong>

<strong><em> </em></strong>

<strong><em> </em></strong>

<strong><em><u>What you are expected to do</u></em></strong> is to

<ol>

 <li>implement the preemptive scheduling system with BH as explained above (and shown in Fig. 1) and</li>

 <li>optimize the quantum <em>q</em>; e., find the quantum value <em>q</em>, such that the average waiting time of BH (<em>AWT</em>) is minimized.</li>

</ol>




<strong><em><u>Process criteria</u> </em></strong>

The waiting time per process <em>i</em>, <em>WT<sub>i</sub></em>, is defined by the sum of all spans of time passed from each arrival time <em>t<sub>arr</sub></em> of process <em>i</em> (assumed to be the time point process <em>i</em> is enqueued) until the time point <em>t<sub>deq</sub></em> it is dequeued (<em>DeleteMin</em>ed) and starts/continues running.




This is mathematically expressed as follows:

<em>K<sub>i</sub></em>




<sub>                          </sub><em>WT</em><em>i </em><sup></sup>(<em>t</em><em><sub>deq</sub></em>(<em>i</em>,<em>k</em>) <em>t</em><em><sub>arr </sub></em>(<em>i</em>,<em>k</em>))

<em>k</em>1

where

<ul>

 <li><em>i</em> is the process index,</li>

 <li><em>k</em> is the index for the BH visits of process <em>i</em> and</li>

 <li><em>K<sub>i</sub></em> denotes the number of times process <em>i</em> is enqueued (i.e., visited BH).</li>

</ul>

<em> </em>

AWT, in turn, is the averaged sum of all individual waiting times, <em>WT<sub>i</sub></em>, or

1 <em>I                                  I      K</em><em>i</em>

1

<em>AWT </em> <em>WT</em><em><sub>i </sub></em> <em>t</em><em><sub>deq</sub></em>((<em>i</em>,<em>k</em>)<em>t</em><em><sub>arr </sub></em>(<em>i</em>,<em>k</em>))

<sub>                                  </sub><em>I </em><em>i</em><sub></sub>1                         <em>I </em><em>i</em><sub></sub>1 <em>k</em><sub></sub>1

with <em>I</em> the total number of processes under consideration over the analysis period.




<strong><em><u>Input:</u> </em></strong>

<ol>

 <li>You will be given a list of triplets (<em>i</em>, <em>e<sub>i</sub></em>, <em>t<sub>arr</sub>(i)</em>) with <em>i</em> the process id, <em>e<sub>i</sub></em>, the execution time and <em>t<sub>arr</sub>(i)</em>, the arrival time of process <em>i</em>. The sequence of triplets in the list specifies the order in which the processes request for processor allocation. You will use the input to compute the priority values <em>f </em>(<em>e</em><em><sub>i </sub></em>,<em>t</em><em><sub>arr </sub></em>(<em>i</em>)) .  These priority values will, in turn, determine the location of each process in BH.</li>

 <li>Source code for a sample binomial heap is available for you. You may modify, compile and use it for your project.</li>

</ol>




<strong><em><u>The computation of </u></em></strong><em>f </em>(<em>e</em><em><sub>i </sub></em>,<em>t</em><em><sub>arr </sub></em>(<em>i</em>)) :

The piecewise continuous function below is used to compute the priority value of process <em>i</em>.




<sup>                                                         </sup><em>c</em>(<em>e</em><em><sub>i </sub></em>)*<em>e</em><em><sub>i </sub></em><em>for e</em><em><sub>i </sub></em> <em>e </em><em><sub>j</sub></em>

<em>f </em><em>e</em><em><sub>i </sub></em>,<em>t</em><em><sub>arr </sub></em>(<em>i</em>)

<sub>                                                         </sub><sub> </sub><em>t</em><em><sub>arr </sub></em>(<em>i</em>) <em>otherwise</em>

<sup>                                                     </sup><sub>           </sub>1                     , for first insertion to BH

          1

<sup>                            </sup><em>with c</em>(<em>e</em><em>i </em>) exp(<sub> </sub>2<em>e</em><em>i </em><sub></sub><sub>3</sub>)    , for further insertions to BH

<sub></sub>

     <sub></sub>3<em>e</em>max <sub></sub>

What this formula says is that, as long as the execution time of process <em>i</em>, <em>e<sub>i</sub></em>, is different than the execution time of any other process <em>j</em>, <em>e<sub>j</sub></em>, the priority of process <em>i</em> is its execution time. In case the execution times of two processes <em>i</em> and<em> j</em> are the same, then the arrival time <em>t<sub>arr</sub>(i)</em> of process <em>i</em> becomes its priority among those jobs with the same execution time <em>e<sub>i</sub></em>.  If process <em>i</em> is inserted to BH for the first time, the factor <em>c(e<sub>i</sub>)</em>=1.  Otherwise (i.e., for further insertions),   <em>c(e<sub>i</sub>)</em> is calculated using the above formula and multiplied to the <u>new</u> execution time, <em>e<sub>i</sub><sup>new</sup></em>, of process <em>i</em> (i.e., <em>(e<sub>i</sub><sup>new</sup> = e<sub>i</sub><sup>pre</sup>– q))</em>.  Note as a programming detail that the original execution time should be stored in the node record. To determine the priority of processes <em>i</em> and<em> j</em>, their arrival times <em>t<sub>arr</sub>(i)</em> and <em>t<sub>arr</sub>(j)</em> are compared.  The sooner the arrival of a process in BH, the higher its priority.




The factor of <em>e<sub>i</sub></em>, <em>c(e<sub>i</sub>)</em>, when <em>e<sub>i </sub>≠</em> <em>e<sub>j</sub></em>, slightly diminishes the priority value of process <em>i</em> with respect to the remaining execution time of process <em>i</em> in case it is preempted before it can finish its execution and reinserted into BH.




<strong><em><u>Algorithm:</u> </em></strong>




<ul>

 <li>Initialize parameters such as <em>q</em>, <em>e<sub>max</sub></em>;</li>

 <li>While there exist processes in the input list o Put the next process <em>i</em> arrived in P o While P allocated

  <ul>

   <li>Enqueue incoming processes by their priority</li>

   <li>If <em>e<sub>i</sub></em>  &gt; <em>q</em></li>

  </ul></li>

 <li>Preempt current process</li>

 <li>Reassign new priority</li>

 <li>Re-insert process into BH</li>

 <li>Else release P</li>

 <li>For each process <em>i</em> in BH</li>

</ul>

 Update <em>WT<sub>i</sub></em>

<ul>

 <li><em>DeleteMin</em> (i.e., remove most prior process from BH)</li>

 <li>Assign P to this process oEnd of While</li>

</ul>

End of While




One potential algorithm is given above for a specific quantum value.  You may, but do not have to, use it.




To accomplish the minimization of <em>AWT </em>over a variety of quantum values, <em>q</em>, you have to iterate the whole run for many increasing/decreasing <em>q</em> values and store the corresponding <em>AWT</em> values. The <em>q</em> value providing the minimum <em>AWT</em> is the value we are looking for. This iteration is not considered in the algorithm given above.




<strong><em><u>A Sample Scenario:</u> </em></strong>

<em> </em>

<em><u>The input file (PID</u></em><u>, <em>e, t<sub>arr)</sub>:</em></u>

P1       3          0

P2       1          2

P3       2          3

P4       2          5

P5       2          6

P6       4          7




The allocation sequence of P for different q values(<strong>e<sub>max</sub>=4</strong>):

<strong>q=1 </strong>

0      1       2       3       4       5       6       7       8        9      10     11     12     13     14

<table width="505">

 <tbody>

  <tr>

   <td width="31">P1</td>

   <td width="36">P1</td>

   <td width="36">P2</td>

   <td width="36">P1</td>

   <td width="36">P3</td>

   <td width="36">P3</td>

   <td width="36">P4</td>

   <td width="36">P4</td>

   <td width="36">P5</td>

   <td width="36">P5</td>

   <td width="36">P6</td>

   <td width="36">P6</td>

   <td width="36">P6</td>

   <td width="36">P6</td>

  </tr>

 </tbody>

</table>

<h1><strong>         </strong><strong>P </strong></h1>

<h2>       Time Processes in BH          Priority value of processes in BH</h2>

<ul>

 <li>P1                         P1: 3</li>

 <li>P1                         P1: (1/exp-(2*2/3*4)<sup>3</sup>)*2 = 2.075</li>

 <li>P1, P2                     P1: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005, P2: 1</li>

 <li>P1, P3                     P1: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005, P3: 2</li>

 <li>P3                         P3: 2</li>

 <li>P3, P4                     P3: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005, P4: 2</li>

 <li>P4, P5                     P4: 5, P5:6 (both have the same <em>e </em>value, so priority is <em>t<sub>arr</sub></em>)</li>

 <li>P4, P5,P6             P4: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005, P5: 2,P6:4</li>

 <li>P5, P6                     P5: 2, P6: 4</li>

 <li>P5, P6                     P5: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005, P6: 4</li>

 <li>P6                         P6: 4</li>

 <li>P6                         P6: (1/exp-(2*3/3*4)<sup>3</sup>)*3 = 3.399</li>

 <li>P6                         P6: (1/exp-(2*2/3*4)<sup>3</sup>)*2 = 2.075</li>

 <li>P6                         P6: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005</li>

 <li>EMPTY</li>

</ul>




<h2>     PID     Waiting time</h2>

P1       1

P2       0

P3       1

P4       1

P5       2

P6       3




AWT = 8/6 = 1.33




























<strong>q=2 </strong>

0      2       3       4       6       8      10     12      14

<table width="408">

 <tbody>

  <tr>

   <td width="51">P1</td>

   <td width="51">P2</td>

   <td width="51">P1</td>

   <td width="51">P3</td>

   <td width="51">P4</td>

   <td width="51">P5</td>

   <td width="51">P6</td>

   <td width="51">P6</td>

  </tr>

 </tbody>

</table>

<h1><strong>             </strong><strong>P </strong></h1>




<h2>       Time Processes in BH          Priority value of processes in BH</h2>

0          P1                                P1: 3

<ul>

 <li>P1, P2                     P1: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005, P2: 1</li>

 <li>P1, P3                     P1: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005, P3: 2</li>

 <li>P3                         P3: 2</li>

</ul>

6          P4, P5                         P4: 5, P5:6 (both have the same <em>e </em>value, so priority is <em>t<sub>arr</sub></em>)

8          P5, P6                         P5: 2, P6: 4

10        P6                                P6: 4

12        P6                                P6: (1/exp-(2*2/3*4)<sup>3</sup>)*2 = 2.075

14        EMPTY




<h2>     PID     Waiting time</h2>

P1       1

P2       0

P3       1

P4       1

P5       2

P6       3




AWT = 8/6 = 1.33




<strong>q=3 </strong>

0           3           4          6           8         10         13         14

<table width="357">

 <tbody>

  <tr>

   <td width="51">P1</td>

   <td width="51">P2</td>

   <td width="51">P3</td>

   <td width="51">P4</td>

   <td width="51">P5</td>

   <td width="51">P6</td>

   <td width="51">P6</td>

  </tr>

 </tbody>

</table>

<h1><strong>          </strong><strong>P </strong></h1>




<h2>       Time Processes in BH          Priority value of processes in BH</h2>

0          P1                                P1: 3

<ul>

 <li>P2, P3                     P2: 1, P3: 2</li>

 <li>P3                         P3: 2</li>

</ul>

6          P4, P5                         P4: 5, P5:6 (both have the same <em>e </em>value, so priority is <em>t<sub>arr</sub></em>)

8          P5, P6                         P5: 2, P6: 4

10        P6                                P6: 4

<ul>

 <li>P6                         P6: (1/exp-(2*1/3*4)<sup>3</sup>)*1 = 1.005</li>

 <li>EMPTY</li>

</ul>




<h2>     PID     Waiting time</h2>

P1       0

P2       1

P3       1

P4       1

P5       2

P6       3




AWT = 8/6 = 1.33





