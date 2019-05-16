# NS-2-Selfish-Behavior-Protocols

Ad-hoc mobile networks (MANETs) are those whose nodes have mobility, energy restriction and which function simultaneously as end systems and router. One of the main problems encountered in MANETs is the occurrence of selfish nodes.

According to [Wankhade](https://pdfs.semanticscholar.org/41e2/a539eb1e96cc6a150e92c8614705cd1c9b2f.pdf) one of the main problems of MANETs networks is the behavior of selfish nodes, which can be defined by the attitudes of obtaining network advantages (eg, flow, watts, among others), especially in packet routing, which consumes a significant amount of energy and not all nodes are willing to spend that precious resource by forwarding packets that are not theirs.

---
# Definition of Selfish Nodes:

The problem of the selfish knot according to [Bakakhouya](https://ieeexplore.ieee.org/abstract/document/4756492) is that it participates in routing functions by agreeing to forward packets on behalf of other nodes, but instead silently discards packets in an attempt to save energy and bandwidth.

* There are two types of us selfish:

<ol>
  <li>which correctly participates in the routing functions, but does not redirect data packets;</li>
  <li>and what does not participate, discarding control messages.</li>
</ol>

> The selfish knot of type 2 has no great effect on the packet delivery rate. However, type 1 is the most damaging to the network by degrading the packet delivery rate.

---
<p>
  <pre><code>
--------------------------------------------------------------
A LGORITHM 1
Selfish Behavior of the AODV,DSDV,DSragent,OLSR, Node.
--------------------------------------------------------------
Input: Data Package or Control.
Output: Routing, Disposal, or Package Processing.
1: if (Data Package) then
2:  if (Data Packet was Originated in the Current Node) then
3:    Forwards(Package);
4:  else
5:    Drop(Package);
6:  end if
7: else
8:  Pass the package to the OLSR for processing;
9: end if
  </code></pre>
</p>

---
# COMO USAR?
Voce precisa ter instalo a versao allinone do ns-allinone-2.34, que esta disponivel no link [tal tal](link), apos feito a compilacao do NS-2 voce tera de adicionar os comandos nos arquivos AODV;DSDV;OLSR;DSR, respectivamente.
 
## Para usar o protocolo AODV, altere os arquivos:

* ns-2.34/aodv/aodv.cc
<p>
  <pre><code>
///entre as linhas 97-98, adicione: 
///Start Sefish Behavior
    if(strcmp(argv[1], "egoista_on") == 0){
	   selfish = true;
	   return TCL_OK;
    } 
    ///Stop Sefish Behavior
    else if(strcmp(argv[1], "egoista_off") == 0){
	   selfish = false;
	   return TCL_OK;
    }
</code></pre>
</p>    

<p>
  <pre><code>
///apos a linha 153, adicione:
///Initializing variable
  selfish = false;
</code></pre>
</p>  

<p>
  <pre><code>
///entre a inha 609-610, adicione:
///Set node's Behavior selfish - By Diógenes
   if(ih->saddr() != index && selfish == true){
	  drop(p, DROP_RTR_SELFISH); //Set as "SEL" in the trace.
	  return; 
  }
  </code></pre>
</p>  

---
* ns-2.34/aodv/aodv.h

<p>
  <pre><code>
	///Na linha 326, adicione:
	///selfish node
	bool selfish;
 </code></pre>
</p> 	 

---
---
## Para usar o protocolo DSDV
* ns-2.34/dsdv/dsdv.cc

<p>
  <pre><code>
///entre as linhas 1060 e 1061, adicione:
     ///Set node's Behavior selfish - By Diógenes
      if(src != myaddr_ && selfish == true && cmh->ptype() != PT_MESSAGE){
	drop(p, DROP_RTR_SELFISH); //Set as "SEL" in the trace.
	return; 
      }
 </code></pre>
</p>      
      
<p>
  <pre><code>
///apos a linha 1099, adicione:
selfish = false;
 </code></pre>
</p>

<p>
  <pre><code>
///entre as linhas 1050 e 1051, adicione:
	///Start Sefish Behavior
      else if(strcmp(argv[1], "egoista_on") == 0){
	   selfish = true;
	   return TCL_OK;
      }  
      ///Stop Sefish Behavior
      else if(strcmp(argv[1], "egoista_off") == 0){
	   selfish = false;
	   return TCL_OK;
    }
 </code></pre>
</p>

---
* ns-2.34/dsdv/dsdv.h

<p>
  <pre><code>
///na linha 140, adicione:  
///selfish node
  bool selfish;
</code></pre>
</p>

---
---
## Para usar o protocolo AODV, altere os arquivos:
* ns-2.34/olsr/olsr.cc

<p>
  <pre><code>
entre as linhas 216 e 217: adicione:
     ///Start Sefish Behavior
    if(strcmp(argv[1], "egoista_on") == 0){
	   selfish = true;
	   return TCL_OK;
    }  
    ///Stop Sefish Behavior
    else if(strcmp(argv[1], "egoista_off") == 0){
	   selfish = false;
	   return TCL_OK;
    }
</code></pre>
</p>

<p>
  <pre><code>
Entre as linha 477 e 478, adicione 
   //Selfish var starting
   selfish = false;
</code></pre>
</p>


`Entre as linha 515 e 516, adicione:
   //Selfish var starting
   selfish = false;`


