- # Notes
	- What is the storage capacity units?
	  collapsed:: true
		- 1 Bit = Binary Digit
		- 8 Bits = 1 Byte
		- 1000 Bytes = 1 Kilobyte $$10^3$$
		- 1000 Kilobytes = 1 Megabyte $$10^6$$
		- 1000 Megabytes = 1 Gigabyte 10^9
		- 1000 Gigabytes = 1 Terabyte (10^12)
		- 1000 Terabytes = 1 Petabyte (10^15)
		- 1000 Petabytes = 1 Exabyte (10^18)
		- 1000 Exabytes = 1 Zettabyte
		- 1000 Zettabytes = 1 Yottabyte
		- 1000 Yottabytes = 1 Brontobyte
		- 1000 Brontobytes = 1 GeopbyteBytes
	- What is major performance measures
	  collapsed:: true
		- capacity (bytes), cost, Bandwidth (bytes/sec), latency (secs, 延迟)
	- **What is CRUD model for storage operations**
	  collapsed:: true
		- Create, Read, Update, Delete
	- **Complete Time =?**
	  collapsed:: true
		- Completion Time = Latency + Size/Bandwidth
		- Small requests will be dominated by latency
		- Big requests will be dominated by bandwidth
	- **Structuring data**
	  collapsed:: true
		- ^^Syntax^^: structure of the data
			- How are the data structured
			- XML, HDF, CSV
		- ^^Semantics^^: meaning of the data
			- what do the data mean
			- ontology, taxonomy, schema
		- Structured: excel spread sheet
		- Unstructured: no predefined data model
		- Semi_structured: JSON, XML Uses metadata to identify specific data characteristics