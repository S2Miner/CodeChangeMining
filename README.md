# SCMiner

This repository contains the mining results of the research paper  "Mining for Structural Similar Code Changes" of ICPC2020.

## Data Structure

* all/ 

In this directory, it mainly contains the clustering results of 111,187 code changes.
All these code changes are extracted from 87 open-source projects on github. All these projects are used in [work of Hoan Nguyen et al.
](https://2019.icse-conferences.org/details/icse-2019-Technical-Papers/39/Graph-based-Mining-of-In-the-Wild-Fine-grained-Semantic-Code-Change-Patterns). 

* all/start-end.json

We have indexed these code changed for 0 to 111,186. Each 1000 of these code changes has been store in file "start-end.json", where **start** corresponds to the smallest id in this file and **end** corresponds to the largest id in this file.

Each method are stored with 6 meta data:

                    id: corresponds to the id of this code change.
                   url: corresponds to the url of the projects from which this code changes is extracted.
             commit_id: corresponds to the id of the commit which commmits this code change.
      original_content: corresponds to the method content before modification.
      modified_content: corresponds to the method content after modficaiton.

* all/clusters.json

This file contains the clustering result of these 111,187 code changes. Each cluster corresponds to a group of similar code changes which we mine from 111,187 code changes. 

Each cluster has been represented with a group of code change ids.
