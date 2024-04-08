<h1 align="center"><img width="300px" src="docs/figures/logo_TRGT.svg"/></h1>

<h1 align="center">TRGT</h1>

<h3 align="center">Tandem repeat genotyping tool for HiFi sequencing data</h3>

TRGT is a tool for targeted genotyping of tandem repeats from PacBio HiFi data.
In addition to the basic size genotyping, TRGT profiles sequence composition,
mosaicism, and CpG methylation of each analyzed repeat. TRGT comes with a
companion tool TRVZ for visualization of reads overlapping the repeats.

## Early version warning

Please note that TRGT is still under active development. We anticipate some
changes to the input and output file formats of both TRGT and TRVZ.

## Availability

- TRGT and TRVZ Linux binaries are [available here](https://github.com/PacificBiosciences/trgt/releases)
- Repeat definition files are available in [this Zenodo repository](https://zenodo.org/record/8329210)
  and definitions of known pathogenic repeats are [also available here](repeats/).

## TRGTdb

TRGT outputs VCFs containing TR alleles from each region in the repeat catalog.
To facilitate analysis of alleles across multiple samples, we provide the TRGTdb
which can be found [here](https://github.com/PacificBiosciences/trgt/pull/6).
After cloning that fork, the TRGTdb can be installed by running
`python3 -m pip install trgt/`. See the fork's `notebooks/` directory for tutorials
converting results into TRGTdb as well as example analyses. TRGTdb was developed by
[Adam English](https://github.com/ACEnglish).

## Documentation

- Tutorials
  - Introductory tutorial: [non-interactive](docs/tutorial.md) and
    [interactive](https://mybinder.org/v2/gh/tandem-repeat-workflows/trgt-tutorial/HEAD?labpath=tutorial.ipynb)
    versions
  - [Interpreting TRVZ plots](docs/trvz-plots.md)
- Reference
  - [Command-line interface](docs/cli.md)
  - [Repeat definition file](docs/repeat_files.md)
  - [VCF files generated by TRGT](docs/vcf_files.md)

## Need help?

If you notice any missing features, bugs, or need assistance with analyzing the
output of TRGT, please don't hesitate to [reach out by email](mailto:edolzhenko@pacificbiosciences.com)
or open a GitHub issue.

## Support information

TRGT is a pre-release software intended for research use only and not for use
in diagnostic procedures. While efforts have been made to ensure that TRGT
lives up to the quality that PacBio strives for, we make no warranty regarding
this software.

As TRGT is not covered by any service level agreement or the like, please do
not contact a PacBio Field Applications Scientists or PacBio Customer Service
for assistance with any TRGT release. Please report all issues through GitHub
instead. We make no warranty that any such issue will be addressed, to any
extent or within any time frame.

## Citation

Please consider citing the paper describing TRGT:

[Dolzhenko E, English A, Dashnow H, De Sena Brandine G, Mokveld T, Rowell WJ,
Karniski C, Kronenberg Z, Danzi MC, Cheung W, Bi C, Farrow E, Wenger A,
Martínez-Cerdeño V, Bartley TD, Jin P, Nelson D, Zuchner S, Pastinen T,
Quinlan AR, Sedlazeck FJ, Eberle MA. Characterization and visualization of
tandem repeats at genome scale. 2024](https://www.nature.com/articles/s41587-023-02057-3)

## Full Changelog

- 0.3.4
  - Improved label spacing in TRVZ plots
- 0.4.0
  - Added TRVZ tutorial
  - Added sample karyotype parameter (`XX` or `XY`)
  - Renamed VCF genotype field `ALCI` to `ALLR`
  - Made genotyping algorithm changes to improve accuracy
- 0.5.0
  - The genotyper now uses information about SNPs adjacent to repeats
  - BAM files now contain read-to-allele assignments
  - Added support for gzip compressed repeat files
  - Improved error handling and error messages
- 0.6.0
  - Add alignment CIGARs to spanning.bam reads
  - Increase read extraction region
  - Cluster genotyper reports confidence intervals
  - Improved error handling of invalid input files (genome, catalog
    and reads)
- 0.7.0
  - Read phasing information can now be used during repeat genotyping (via `HP` tags)
  - Users can now define complex repeats by specifying motif sequences in the MOTIFS field and setting STRUC to <`locus_name`>
  - The original MAPQ values in the input reads are now reported in the BAM output
  - BAMlet sample name can now be provided using the `--sample-name` flag; if it not provided, it is extracted from the input BAM or file stem (addressing issue #18)
- 0.8.0
  - **Breaking change**: Motif spans and counts (`MS` and `MC` fields) and purity assessment (`AP`
    field) are now performed with an HMM-based algorithm for all repeats; expect
    some differences in results relative to the previous versions
  - Allele purity of zero-length alleles are now reported as missing values in
    the VCFs
  - The spanning.bam output file now carries over the QUAL values and mapping
    strand from the input reads
  - Added an advanced flag `--output-flank-len` that controls the number of
    flanking bases reported in the spanning.bam files and shown in trvz plots
  - A crash that may occur on BAMs where methylation was called twice has been
    fixed
  - Optimizations to the `--genotyper=cluster` mode, including haploid genotyping
    of the X chromosome when `--karyotype` is set to `XY`
- 0.9.0
  - Add support for polyalanine repeats (by allowing characters `N` in the motif sequence)
  - Fix a bug causing TRVZ to error out on polyalanine repeats

### DISCLAIMER

THIS WEBSITE AND CONTENT AND ALL SITE-RELATED SERVICES, INCLUDING ANY DATA, ARE
PROVIDED "AS IS," WITH ALL FAULTS, WITH NO REPRESENTATIONS OR WARRANTIES OF ANY
KIND, EITHER EXPRESS OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, ANY WARRANTIES
OF MERCHANTABILITY, SATISFACTORY QUALITY, NON-INFRINGEMENT OR FITNESS FOR A
PARTICULAR PURPOSE. YOU ASSUME TOTAL RESPONSIBILITY AND RISK FOR YOUR USE OF THIS
SITE, ALL SITE-RELATED SERVICES, AND ANY THIRD PARTY WEBSITES OR APPLICATIONS. NO
ORAL OR WRITTEN INFORMATION OR ADVICE SHALL CREATE A WARRANTY OF ANY KIND. ANY
REFERENCES TO SPECIFIC PRODUCTS OR SERVICES ON THE WEBSITES DO NOT CONSTITUTE OR
IMPLY A RECOMMENDATION OR ENDORSEMENT BY PACIFIC BIOSCIENCES.
