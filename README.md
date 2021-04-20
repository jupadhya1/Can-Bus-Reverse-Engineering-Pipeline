# Can-Bus-Reverse-Engineering-Pipeline

	Data Collection	Lexical Analysis	Semantic Analysis
Input	Driving Route 
Driving Conditions Driver Input	Output of Data Collection	Output of Data Collection
Output	- Arbitration IDs
 - Payloads	- Payload Compositions 
- Time Series (Signals	- Correlated Relationships
 - Causal Relationships
 - Predictive Models


This project houses Python and R scripts intended to facilitate the automated reverse engineering of Controller Area Network (CAN) payloads observed from passenger vehicles. 

Pipeline
Input: CAN data in the format demonstrated in LoggerProgram0.log
•	Main.py
i.	Purpose: This script links and calls all remaining scripts in this folder. It handles some ‘global’ variables used for modifying the flow of data between scripts as well as any files output to the local hard disk.
•	PreProcessor.py
i.	Purpose: This script is responsible for reading in .log files and converting them to a runtime data structure known as a Pandas Data Frame. Some ‘data cleaning’ is also performed by this script. The output is a dictionary data structure containing ArbID runtime objects based on the class defined in ArbID.py. J1979.py is called to attempt to identify and extract data in the Data Frame related to the SAE J1979 standard. J1979 is a public communications standard so this data does not need to be specially analysed by the following scripts.
•	LexicalAnalysis.py
i.	Purpose: This script is responsible for making an educated guess about the time series data present in the Data Frame and ArbID dictionary created by PreProcessor.py. Individual time series are recorded using a dictionary of Signal runtime objects based on the class defined in Signal.py.
•	SemanticAnalysis.py
i.	Purpose: This script generates a correlation matrix of Signal time series produced by LexicalAnalysis.py. That correlation matrix is then used to cluster Signal time series using an open-source implementation of a Hierarchical Clustering algorithm.
•	Plotter.py
i.	Purpose: This script uses an open-source plotting library to produce visualizations of the groups of Signal time series and J1979 time series produced by the previous scripts.
Output: This series of scripts produces an array of output depending on the global variables defined in Main.py. This output may include the following:
•	‘Pickle’ files of the runtime dictionary and Data Frame objects using the open-source Pickle library for Python. These files simply speed up repeated execution of the Python scripts when the same .log file is used for input to Main.py.
•	Comma separated value (.csv) plain text files of the correlation matrix between time series data present in the .log file.
•	Graphics of scatterplots of the time series present in the .log file.
•	A graphic of the dendrogram produced during Hierarchical Clustering in SemanticAnalysis.py. A dendrogram is a well-documented method for visualizing the results of Hierarchical Clustering algorithms.

