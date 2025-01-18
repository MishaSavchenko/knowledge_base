# Finite State Machines (FSM)

Refs: [wiki](https://en.wikipedia.org/wiki/Finite-state_machine)

* Abstract machine that can be in exactly one state of a finite number of states  
* Transition  
  * Change from one state to the another  
* Deterministic Finite-State Machines   
  * Can be constructed equivalent to any non-deterministic state machine  
* Non-Deterministic Finite-State machines  
* Less computation power than Turing Machines  
* FSM memory is limited by the number of state it has  
* Automata Theory and theory of computation studies FSMs   
* State-transition tables, Directed graph, State diagram   
  * Used to represent an FSM  
* Usage   
  * Modeling reactive systems   
  * Electrical engineering  
  * Linguistics  
  * Computer Science  
    * Hardware digital systems   
    * Software engineering   
    * Compilers   
    * Network protocols   
    * Study of computation and languages  
  * Philosophy  
  * Biology  
  * Mathematics   
  * Logic 

### Concepts and Terminology 

* State  
  * Description of the status of a system, waiting to execute a transition  
* Transition   
  * Set of actions to be executed when a condition is fulfilled  
* Identical stimuli trigger different actions depending on the current state  
* Entry Action  
  * Performed when entering the state  
* Exit Action   
  * Performed when exiting the state

### Representations 

* State/Event Table  
  * Several types   
  * Complete action’s information no directly described  
* UML State Machines  
  * UML has notation for FSMs   
  * Have the characteristics of both Mealy and Moore machines  
  * Introduce  
    * hierarchically nested states  
    * orthogonal regions  
    * Expending actions  
      * State and triggering event dependent actions are supported (Mealy Machines)  
      * Entry and Exit Action (Moore Machines)  
* SDL State Machines  
  * Specification and Description Language  
  * Include graphical Symbols to describe actions in the transition   
  * Abstract Data Types

### Classification 

* FSMs can be subdivided into the following 

#### Acceptors (/detectors/recognizers)

* Produce binary output to indicate whether input has been received   
* Each state is either   
  * Accepting   
  * Non Accepting   
* Once input has been received the input is accepted (otherwise its rejected)   
* Input is a characters   
* Actions not used   
* Could be described as defining a language that would contain every string accepted, but non of the rejected ones   
  * Languages accepted by Acceptors are **regular languages**  
*   

#### Classifiers  

* Acceptors that produce n-ary output where n is strictly greater than two   
*  

#### Transducers

* Output based on a given input and/or state using actions   
* Moor Machine   
  * Uses only entry actions  
    * Output depending only on the sate  
  * Simplification of the behaviour  
* Mealy Machine  
  * Uses input actions   
    * Output depends on input and state  
  * Often leads to reduction of \# of states  

#### Sequencers 

* Subclass of acceptors and transducers  
* Single letter input alphabet   
* Proceed only one sequence which can be seen as an output sequence of acceptor or transducer outputs

#### Determinism 

* Deterministics  
  * Every state has exactly one transition for each possible input   
* Non-deterministic   
  * An input can lead to one, none, or more than one transition for a given state  
* Powerset construction algorithm can transform any non deterministic automaton into a deterministic automaton with identical functionality 