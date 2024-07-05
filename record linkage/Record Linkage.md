# What is Record Linkage 
- The task of finding records in a data set that refer to the same entit across data sources 
- necessary when joining different data sets which may not have a common identifier
- also referred to :
	- computer science:
		- data matching
		- object identify problem
	- commercial mail and database applications
		- merge/purge processing
		- list washing
	- other
		- coference/entity/identity/name/record resolution
		- entity disambiguation/linking
		- fuzzy matching
		- duplicate detection
		- deduplication
		- record matching
		- (reference) reconciliation
		- object identification
- data preprocessing is important because the quality of the data being linked will impact the success of the record linkage, ie, key identifiers for the same entity can be presented differently between (and even within datasets), such as variations in name william j smith v smith, w.j, bill smith 
# Deterministic Record Linkage
- #DeterministicRecordLinkage or #Rules-BasedRecordLinkage is the simplest kind of linkage 
	- generates links based on the number of individual identifiers that match among the available data sets
	- two records are said to match if the identifiers are identical
	- thisi s a good option when the entities in the datasets are identified by a common identifier or when there are several representative identifiers (name, dob, sex, for a person) whose quality of data is very high 
	- however, a decrease in data quality or small increase in the complexity of data can result in a large increase in the number of rules necessary to link records properly
# Probabilistic Record Linkage
- sometimes called #FuzzyMatching or #ProbabilisticMerging or #FuzzyMerging takes into account a wider range of potential identifiers, computing he weights on its estimated ability to correctly identify a match or a non-match and then uses the weights to calculate a probability that two given records refer to the same entity 
- can be trained to perform (as opposed to a series of potentially complex rules to be programmed ahead of time)