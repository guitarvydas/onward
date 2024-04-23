Container and Leaf Components
The diagram in Figure \ref{mot} represents two (2) kinds of components.
The main diagram is, itself, a component. It is a Container which displays its implementation in diagrammatic form as a composition of four other components with connections between them.
Containers can contain other Containers or other Leaf components. In this very simple example, the child components happen to all be Leaf components and, happen to all be derived from the same template - “Echo”. In more practical drawings, this is not usually the case - Containers generally contain components derived from a variety of templates
Leaf components contain executable code. Leaves do not contain other components.
Children components are drawn as rectangles and contain other, smaller rectangles representing input and output ports for each child component.
Connections are one-way and are drawn as arrows. Line width and style are ignored in this DPL. This allows software architects to choose graphic representations on a per-project basis, emphasizing certain aspects of the design and deemphasizing other aspects. In this example, we used 2pt line thickness to indicate “important” connections. Note that implementing bi-directional connections requires extra software while obfuscating elements of the design.
Input and output ports of the diagram - “gates” - are drawn as rhombuses. 
The kind of each port or gate is determined by how arrows are attached to it. A port that has an arrowhead attached to it is an “input port”, while “output ports” have arrowtails attached to them. Gates, though, are opposite in sense. Gates that have arrowheads attached to them are “output gates” while gates that have arrowtails attached to them are “input gates”.
All rectangles and rhombuses can have one text string associated with them. The text string is contained within the rectangles. Names represent template classes for components. For ports and gates, names are tags that are used by components to signify the kind of messages being received and sent. Note that empty strings are legal names and are reserved to mean UNIX®-like standard inputs and standard outputs.
The reader might notice a resemblance of this DPL with electronic components. In electronics, components are called “ICs”, and ports are called “pins”. Container diagrams are called “schematics”. ICs are black boxes encased in epoxy or plastic. One cannot peer “inside” of any IC to determine how it is implemented. Templates are called “data sheets”. Components in this DPL and electronics ICs share the characteristic that they are completely asynchronous and completely isolated from one another. In contrast, software \emph{functions} and \emph{libraries} are tightly coupled and synchronous. Functions imply ad-hoc blocking - the caller must block indefinitely waiting for a response from the callee, and, the caller cannot rely on timing characteristics of callees due to the fact that callees can call other callees synchronously and block waiting for their response. 
Each component instance - whether Container or Leaf - has exactly one input queue and exactly one output queue.
A key feature of any DPL is that components are truly isolated from one another due to the use of FIFO queues instead of reliance on LIFO callstacks. This conforms with common human understanding of the operation of drawings, objects and actors. Other aspects of DPLs contribute to component isolation, in particular the use of input and output queues and the restrictions on message routing (components cannot direct messages to other components - this is handled solely by their parent Containers).
One cannot determine “from the outside” whether a component is a Container or a Leaf, nor know anything about its implementation. One cannot know if a component contains state or is a pure function. In fact, knowledge of these kinds of details is unnecessary. Programmers can dig deeper into the innards of components if they want to know such low-level details.
Components process each incoming message. Processing is based on internal component state and the port tag contained in a message. A message is a 2-tuple {port X payload}.
Output message processing consists of placing tagged messages {tag X payload} onto the component’s (single) output queue. Output messages are sent in a deferred manner. Output messages sit in a component’s output queue until the component has finished processing a step of its potential actions and returns control back to its parent (always a Container). The parent container empties a child’s output queue and routes messages in first to last order of output message creation (note that “recursion” works oppositely, in a last to first order - most recent first).
Output queues contain messages with port tags that are relative to the \emph{sender}. Input queue contains messages with port tags that are relative to the \emph{receiver}. Routers, i.e. Containers, must map from output tag of the sender to the appropriate input tags of the receivers.
Component instances need not be explicitly named. Their (x,y) position on a diagram uniquely identifies each instance. Thisagrees with normal human convention - visual placement on the diagram has semantic meaning.
Fan-in and fan-out are supported. Fan-in means that a single input port/gate can receive messages from multiple sources. This is straight-forward to implement using the FIFO queue structure of components. Fan-out, though, means that a single port/gate can send messages to several receivers. This requires copying of message payloads or the application of copy-on-write semantics in the receivers. There is no semantic difference between these two techniques - the choice of implementation (copying vs. copy-on-write) is purely one of optimization and does not matter at the design stages. Efficiency of implementation matters only during Production Engineering stages, i.e. when a design is stable enough to be productized.
Fan-out may be an inconvenience in the theoretical sense, but, is a vital feature for usability of DPLs. For example, fan-out makes it possible to abstract diagrams by grouping components together and pushing them over onto other diagrams, leaving only a single component with fewer ports on the originating diagram. This kind of usage is fundamental to one’s being able to layer a design in meaningful ways. In contrast, function-based programming relies on a single expression for layering - the function (aka “lambda”). The paucity of expression in function-based-only-programming leads to obfuscation of design intent (“DI”) and makes designs appear more complicated than necessary to casual readers.

Connections are triples {direction X sender X receiver}.

In this DPL, there are four (4) connection directions
\begin{itemize}
\item down
\item across
\item up
\item through.
\end{itemize}

The sender information in connections must include a reference to a component instance and a port.
The receiver information in connections must include a reference to a component instance and a port.

Structure of connection triples {dir,sender,receiver}


- Breakdown of Figure 1 Container information.
- Need for fan-out
- layering, functions == only way to achieve abstraction and layering in FP, leading to a paucity of design expression
