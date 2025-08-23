<iframe 
	  width="100%"
	  height="500"
	  src="https://gboisse.github.io/posts/node-graph">
</iframe>



- root nodes representing the origin of the graph traversal is really interesting, partially because i never thought about it like that, but roots can also represent different thread or processes that needs to be executed.
	- the system can contain multiple trees which pass data to each at "synchronization point" 
	- data + component nodes are much clearer construction than the whatever moveit task constructor tried to pull out of their ass  (im just frustrated)
> [!question] What was the reason behind the MTC doing their tasks in the way they did, instead of trying to use something the construct above?

