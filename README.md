bio_assembly_refinement
=======================

Pipeline to filter, trim, circularise and re-assemble contigs, mostly useful for (but not limited to) draft bacterial assemblies using long read data (e.g. PacBio)

Description
-----------

Given a fasta file, these modules can be used to:

1. Filter out contigs smaller than a set length, and those completely contained within other contigs
2. Identify and trim overlaps between ends of contigs
2. Circularise contigs by setting its start to be the start of the conserved dnaA gene (or other genes in the case of plasmids) 
3. Run quiver (pacbio_smrtanalysis script) on the new circularised contigs to refine them, particularly around the new joins

There are also scripts that can be used to call these functions is on the command line

Installation
------------

**Pre-requisites**

*1.	MUMmer*

Instructions to install MUMmer can be found [here](http://mummer.sourceforge.net/manual/#installation)
    
*2.	pacbio_smrtanalysis*

[Installation instructions to be completed]

*3.	pyfastaq*
		
Install: 
	
	pip3 install pyfastaq
		
*4.	prodigal* 
		
PRODIGAL gene finding software. [Installation instructions](https://github.com/hyattpd/prodigal/wiki/Installation) for PRODIGAL 


Usage (for developers)
----------------------

Sample usage of main module:

	from bio_assembly_refinement import main 
	processor = main.Main(fasta_file = input_file, 
					      dnaA_sequence = dnaA_file,
					      bax_files = data_dir
					   	 )
	processor.process_assembly()


Attributes of Main.py:
----------------------

**fasta_file**: input fasta file

**dnaA_sequence**: fasta file with dnaA/refA/refB sequences
 
**bax_files**: directory containing bax.h5 files

**cutoff_contig_length**: minimum contig length (default 10000)

**contained_percent_match**: minimum percent identity in nucmer hits to determine if contig is contained in another (default 95)

**overlap_offset**: offset from the ends of a contig where an overlap region can begin (default 1000)

**overlap_boundary_max**: maximum boundary of the overlap between ends (expressed as % of contig length) (default 50)

**overlap_min_length**: minimum length of overlap (default 1000 bases)

**overlap_max_length**: maximum length of overlap (default 3000 bases)

**overlap_percent_identity**: minimum percent identity in nucmer hits to use when determining if ends overlap (default 85)

**min_trim_length**: minimum trimmed length of contig over total contig length (default 0.8)

**trim**: trim overlaps (default true) 

**trim_reversed_overlaps**: trims overlaps even if reversed (default false)

**dnaA_hit_percent_identity**: minimum percent identity to consider when looking at hits to dnaA/refA/refB (default 80)

**dnaA_hit_length_minimum**: minimum length of hit to dnaA/refA/refB expressed as % of length of dnaA/refA/refB (default 95)

**working_directory**: working directory (default current working directory) 

**pacbio_exec**: pacbio resequencing exec (default pacbio_smrtanalysis) 

**nucmer_exec**: nucmer exec (default nucmer) 

**reassembly_dir**: directory sent to quiver (default reassembly)

**summary_file**: summary file (default pacbio\_postprocess\_summary.txt) 

**debug**: do not delete temp files if set to true (default false)

More documentation available in the code.


Contact
-------

Author: Nishadi De Silva

Affiliation: Wellcome Trust Sanger Institute, Hinxton, UK

Email: path-help@sanger.ac.uk
      
