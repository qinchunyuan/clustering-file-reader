# clustering-file-reader

# Introduction
clustering-file-reader is a library for parsing the clustering output produced by either [spectra-cluster](https://github.com/spectra-cluster/spectra-cluster) or [spectra-cluster-hadoop](https://github.com/spectra-cluster/spectra-cluster-hadoop) library.
The clustering result file is compact text file format which contains all the information related to clusters, these can include the consensus spectrum, precursor details, and spectrum related details.
This library supports parsing both the entire file and iterate over all the entries in a particular file

# Getting started

### Installation
You will need to have [Maven](http://maven.apache.org/) installed in order to build and use the spectra-cluster library.

Add the following snippets in your Maven pom file:

```maven
<!-- spectra-cluster dependency -->
<dependency>
    <groupId>uk.ac.ebi.pride.spectracluster</groupId>
    <artifactId>clustering-file-reader</artifactId>
    <version>${current.version}</version>
</dependency>
```

```maven
 <!-- EBI repo -->
 <repository>
     <id>nexus-ebi-repo</id>
     <url>http://www.ebi.ac.uk/intact/maven/nexus/content/repositories/ebi-repo</url>
 </repository>

 <!-- EBI SNAPSHOT repo -->
 <snapshotRepository>
    <id>nexus-ebi-repo-snapshots</id>
    <url>http://www.ebi.ac.uk/intact/maven/nexus/content/repositories/ebi-repo-snapshots</url>
 </snapshotRepository>
```

### Running the library
TBD

# File format specification
The ".clustering" file format is text based. 

The first lines contain an optional header specifying properties of the algorithm and the sample set.
Each line contains one property where the property's name is separated by an "=" from the value.

Clusters start with the line "=Cluster=". 
The next lines contain the cluster's properties, one property per line where the property's
name is separated by an "=" from the value. Cluster properties are:
1) av_precursor_mz: the average precursor m/z
2) av_precursor_intensity: the average precursor intensity
3) sequence: List of sequences of the peptides identified in the cluster in the format "[{sequence}:{count}]"
4) consensus_mz: ',' delimited m/z values of the consensus spectrum
5) consensus_intens: ',' delimited intensity values of the consensus spectrum

Spectra are defined one line per spectrum containing 'tab' delimited fields. A spectrum line must start
with the term "SPEC". The following fields are: 
1) spectrum's id
2) whether this spectrum was identified as the most common peptide in the cluster ("true" / "false")
3) The identified sequence. If multiple ranks are reported, sequences must be sorted by rank and delimited by an ","
4) Spectrum's precursor's m/z
5) Spectrum's charge
6) Species (taxid), ',' delimited
7) Modifications in the format "[position]-[accession]". Multiple modifications must be separated by an ",". If multiple PSMs are reported these modification groups must be separated by an ";".
8) The similarity of the spectrum (based on the used similarity metric) to the cluster's consensus spectrum

# Getting help
If you have questions or need additional help, please contact the PRIDE Help desk at the EBI.

email: pride-support at ebi.ac.uk (replace at with @).

# Giving your feedback
Please give us your feedback, including error reports, suggestions on improvements, new feature requests. You can do so by opening a new issue at our [issues section](https://github.com/spectra-cluster/clustering-file-reader/issues)

# How to cite
Please cite this library using one of the following publications:
- Griss J, Foster JM, Hermjakob H, Vizcaíno JA. PRIDE Cluster: building the consensus of proteomics data. Nature methods. 2013;10(2):95-96. doi:10.1038/nmeth.2343. [PDF](http://www.nature.com/nmeth/journal/v10/n2/pdf/nmeth.2343.pdf),  [HTML](http://www.nature.com/nmeth/journal/v10/n2/full/nmeth.2343.html),  [PubMed](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3667236/)

# Contribute
We welcome all contributions submitted as [pull](https://help.github.com/articles/using-pull-requests/) request.

# License
This project is available under the [Apache 2](http://www.apache.org/licenses/LICENSE-2.0.html) open source software (OSS) license.
