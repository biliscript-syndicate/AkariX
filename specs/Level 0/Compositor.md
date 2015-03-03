Compositor Layer
================

The compositer layer consists of following interfaces.

INodeType
---------

INode represent a node type. A node type can expose various parameters that can be connected from both directions, forming a pipeline to represent various MG constructs. Various classes in the Implementation Layer implementing INodeType form the feature set of AkariX.

* Properties

    * input : < name : string, type : string, default : * >[]

        Input parameter fields for the node.

    * output : < name : string, type : string >[]

        Output parameter fields for the node.

    * stateful : bool

        Whether the type of node appear stateful in a single iteration. `stateful` nodes are evaluated each time an output is requested, and get access to a iteration term persistent cache.

* Methods

    * evaluate( input : function( string ), output : Hash<string, *>, linkage : Hash<string, Boolean>, cache : Hash<string, *>, iCache : Hash<string, *> ) : void

        Evaluates a node of the type. Input data is requested by calling the given `input` function with parameter name. It is so to avoid evaluating unused nodes. The function should modify the `output` hash passed to it.

        `linkage` includes information about connections to the output slots. Provided that a node offers multiple outputs, only a part of them might be needed. Expensive operations can therefore be avoided if no one needs the output.

        `cache` is a Hash where implementation specific persistent objects can be stored. For example temporary surfaces used by renderers and effects. `iCache` is similiar to `cache` but the data is persistent for only one iteration, provided that `stateful` is `true`. Otherwise, `iCache` is not passed to the method.

    * dispose( output : Hash<string, *>, cache : Hash<string, *> ) : void

        This is called when associated objects need to be disposed. i.e. Compositor dispose.

    * iterationDispose( iCache : Hash<string, *> ) : void

        Same purpose as `dispose`. but called at the beginning of each iteration for `stateful` nodes.

The compositer layer consists of following classes.

Compositor
----------

Compositor reads and presents content as is declared in the composition tree passed to it.

* Properties

    * isActive : bool

        Whether the compositor is active now.

* Methods

    * initialize( tree : CompositionTree ) : void

        Initializes the CompositionTree passed and sets the compositor to active.

    * dispose() : void

        Dispose the current composition tree.

NodeData
--------

* Properties

    * type : string

        Name of the interface that the INode to be assigned to this NodeData implements.

    * links : Hash<string, < target : int, targetOutput : string >>

        Links from this node's input parameter.

    * input : Hash<string, *>

        Values to be substituded to each parameter when no connection is present.

    * iteration : number

        The number of iteration when the node is last evaluated. This is to avoid unnecessary evaluation of nodes when accessed for multiple times.

    * output : Hash<string, *>

        The current output of the node.

CompositionTree
---------------

Representation of a composition tree.

* Properties

    * nodes : NodeData[]

        A list of all nodes in the composition tree.

    * entryPoint : int

        Index of the entry node.