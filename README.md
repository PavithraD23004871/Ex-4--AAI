<H3>NAME : Pavithra D</H3>
<H3>REGISTER NO : 212223230146</H3>
<H3>EX. NO.4</H3>
<H3>DATE: 05.08.2026</H3>
<H1 ALIGN =CENTER> Implementation of Hidden Markov Model</H1>

## Aim: 
Construct a Python code to find the sequence of hidden states by the known sequence of observances using Hidden Markov Model. Consider two hidden states Sunny and Rainy with observable states,happy and sad.

## Algorithm:

Step 1:Define the transition matrix, which specifies the probability of transitioning from  one hidden state to another.<br>
Step 2:Define the emission matrix, which specifies the probability of observing each possible observation given each hidden state.<br>
Step 3:Define the initial probabilities, which specify the probability of starting in each possible hidden state.<br>
Step 4:Define the observed sequence, which is the sequence of observations need to  be analyzed.<br>
Step 5:Initialize the alpha matrix with zeros, where each row represents a time step and each column represents a possible hidden state.<br>
Step 6:Calculate the first row of the alpha matrix by multiplying the initial  probabilities by the emission probabilities for the first observation.<br>
Step 7:Loop through the rest of the observed sequence and calculate the rest of the alpha matrix by multiplying the emission probabilities by the sum of the product of 
       the previous row of the alpha matrix and the corresponding row of the transition matrix.<br>
Step 8:Calculate the probability of the observed sequence by summing the last row of the alpha matrix.<br>
Step 9:Find the most likely sequence of hidden states by selecting the hidden state with the highest probability at each time step based on the alpha matrix.<br>

## Program:
```pq
#Implementation of Hidden Markov Model
import numpy as np
import networkx as nx
import matplotlib.pyplot as plt
'''priorprobs=np.array([0.5,0.1,0.4])
transitionprobs=np.array([[0.5,0.3,0.2],[0.4,0.2,0.4],[0,0.3,0.7]])
emissionprobs=np.array([[0.9,0.1],[0.6,0.4],[0.2,0.8]])
observationseq=np.array([1,1,0])
'''
priorprobs=np.array([0.8,0.2])
transitionprobs=np.array([[0.7,0.3],[0.4,0.6]])
emissionprobs=np.array([[0.2,0.4,0.4],[0.5,0.4,0.1]])
observationseq=np.array([2,0,2])
observations=[]
for i in range(len(observationseq)):
    if observationseq[i]==0:
        observations.append("1 Icecream \n Day "+str(i))
    elif observationseq[i]==1:
        observations.append("2 Icecreams \n Day "+str(i))
    elif observationseq[i]==2:
        observations.append("3 Icecreams \n Day "+str(i))
alpha=np.zeros((len(observationseq),len(priorprobs)))
print(alpha)
alpha[0,:]=priorprobs*emissionprobs[:,observationseq[0]]
print(alpha)
for i in range(1,len(observationseq)):
    for j in range(len(priorprobs)):
        alpha[i,j]=emissionprobs[j,observationseq[i]]*np.sum(alpha[i-1]*transitionprobs[:,j])
print(alpha)
stateseq=[]
for i in range(len(observationseq)):
    t=np.argmax(alpha[i])
    if t==0:
        stateseq.append('Hot '+str(i))
    elif t==1:
        stateseq.append('Cold'+str(i))
        
'''
    else:
        stateseq.append('sunny')
'''
print(stateseq)
edges=[]
colormap=[]
for i in range(len(stateseq)-1):
    edges.append((stateseq[i],stateseq[i+1]))
for i in range(len(stateseq)):
    edges.append((stateseq[i],observations[i]))
pos={}
p=0
for x in stateseq:
    pos[x]=(p,0)
    p+=2
    colormap.append("lightgreen")
t=0
for x in observations:
    pos[x]=(t,-1)
    t+=2
    colormap.append("yellow")


    

#Drawing Graphs
G=nx.DiGraph()
G.add_nodes_from(stateseq)
G.add_edges_from(edges)
nx.draw(G,with_labels=True,node_size=6000,node_color=colormap,pos=pos)
plt.show()
```

## Output:

<img width="802" height="685" alt="image" src="https://github.com/user-attachments/assets/c70172f3-4d6e-4b45-8d4e-837125d4fe33" />


## Result:
Thus Hidden Markov Model is implemented using python.

