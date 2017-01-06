# Deep autoencoders


# Semantic Hashing

- Using a deep autoencoder as a hash-function for finding *approximate* matches.

## Overview
- Fast retrieval methods typically work by interesting stored lists that are associated with cues extracted from the query.
- Computers have special hardware(memory bus) that can intersect 32 very long lists in one instruction.
	- Each bit in a 32-bit binary code specifies a list of half the addresses in the memory
- Semantic hashing uses machine learning to map the retrieval problem onto the type of list intersection the computer is good at.
