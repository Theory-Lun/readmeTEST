# Haplotype Network Construction and Lineage Assignment for SARS-CoV-2

<div style='display: none'>
https://c.runoob.com/front-end/712
![logo](./Logo/logo.png)
</div>

[comment]: <> (asdf)

## Introduction

XXX is a tool for haplotype network construction and lineage assignment for SARS-CoV-2 sequencies. The onlion version will be found here https://ngdc.cncb.ac.cn/ncov/haplotype/.

## Compiling

XXX can be build on most Linux systems. Please build the following headers:
1. igraph C library: https://igraph.org/
2. cJSON: https://github.com/DaveGamble/cJSON.git
3. hashmap: https://github.com/DavidLeeds/hashmap.git

and install

1. Anaconda: https://www.anaconda.com/
2. python_igraph: `pip install python_igraph` or `pip3 install python_igraph`
3. cmake ( >3.19 )

for compiling and running XXX. And then compile network construction part by doing follows:
```
cd .../HapNet/Network
mkdir build
cd build
make ..
cmake
```
For compiling clustring part, please doing follows:
```
cd .../HapNet/Lineage
make
```
## Usage && Examples
For testing XXX, please doing this:
```
cd .../HapNet/Example
mkdir rlt
./run
```
The results will be generated in `.../HapNet/Example/rlt`. The pre-runned results would be found in `.../HapNet/Example/rlt_example`.

The parameters would be reset in `.../HapNet/Example/run`. Here's the description of all parameters:

| Parameters | Description | Example |
| ---- | ---- | ---- |
| output_folder | output path, must exist, must not end with '/' | -  |
| input_mut  | input mutation file | - |
| input_meta  | input metadata file | - |
| HapNetPath  | path of HapNet, must not end with '/' | - |
| ref | accesion ID of reference sequence |  EPI_ISL_454904  |
| out_number | number of samples select from input mutation randomly | 1000 |
| start_time  | filter out samples sampled before this date  | 2019-1-1  |
| end_time  | filter out samples sampled after this date | 2023-5-31  |
| time_accuracy | month: filter out samples without month of sampling time; day: filter out samples without day of sampling time  |  month  |
| country  | filter out other countries for construct haplotype network, must wrapped in quotation marks; ignore this step by setting this parameter to "N/A"  | "China"
| min_freq | the minimum frequence of mutation rate, must be a number between 0 and 1| 0.01 |

## Input Format

Metadata and mutation data are need for construct haplotype network and assign lineage. Metadata must include Accession ID, sampling date and sampling location (country) split by '\t'. Here's an example:
```
EPI_ISL_770734	2020-10-12	Germany
EPI_ISL_412900	2019-12-30	China
EPI_ISL_414594	2020-03-05	United States
EPI_ISL_414619	2020-03-07	United States
MN908947.3	2019-12-30	China
EPI_ISL_431944	2020-04-01	United Kingdom
EPI_ISL_431964	2020-04-02	United Kingdom
EPI_ISL_432090	2020-04-02	United Kingdom
EPI_ISL_432094	2020-04-03	United Kingdom
EPI_ISL_432119	2020-04-01	United Kingdom
EPI_ISL_432128	2020-04-03	United Kingdom
EPI_ISL_432131	2020-04-01	United Kingdom
EPI_ISL_432133	2020-04-04	United Kingdom
EPI_ISL_432136	2020-04-01	United Kingdom
```
Mutation data must include Virus Strain Name, Accession ID and mutations. Here's an example:
```
2019-nCoV_HKU-SZ-002a_2020	MN938384	1(Deletion:AATTAAAGGTTTATACCTTCCCAGGTAACAAAC->-);8782(SNP:C->T);28144(SNP:T->C);29095(SNP:C->T);29870(Deletion:CAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA->C)
2019-nCoV_HKU-SZ-005b_2020	MN975262	8782(SNP:C->T);9561(SNP:C->T);15607(SNP:T->C);28144(SNP:T->C);29095(SNP:C->T);29891(Deletion:AAAAAAAAAAAAA->A)
2019_nCoV Muc IMB1	LR824570	1(Indel:A->GATCGAAAGTTGA);241(SNP:C->T);3037(SNP:C->T);23403(SNP:A->G);29888(Deletion:AAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-AZ1/2020	MN997409	8782(SNP:C->T);11083(SNP:G->T);28144(SNP:T->C);29095(SNP:C->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CA1/2020	MN994467	1548(SNP:G->A);8782(SNP:C->T);24034(SNP:C->T);26729(SNP:T->C);28077(SNP:G->C);28144(SNP:T->C);28792(SNP:A->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CA2/2020	MN994468	17000(SNP:C->T);26144(SNP:G->T);29883(Deletion:AAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CA3/2020	MT027062	614(SNP:G->A);5084(SNP:A->G);28854(SNP:C->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CA4/2020	MT027063	614(SNP:G->A);5084(SNP:A->G);28854(SNP:C->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CA5/2020	MT027064	2091(SNP:C->T);21707(SNP:C->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CA9/2020	MT118835	9924(SNP:C->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CruiseA-19/2020	MT184907	11083(SNP:G->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CruiseA-21/2020	MT184908	254(SNP:C->T);11083(SNP:G->T);29736(SNP:G->T);29751(SNP:G->C);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CruiseA-22/2020	MT184909	11083(SNP:G->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CruiseA-23/2020	MT184910	254(SNP:C->T);1911(SNP:C->Y);9157(SNP:T->C);11083(SNP:G->T);22104(SNP:G->T);29736(SNP:G->T);29751(SNP:G->C);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CruiseA-24/2020	MT184911	1063(SNP:C->Y);3099(SNP:C->T);10083(SNP:C->Y);10507(SNP:C->T);11083(SNP:G->T);15193(SNP:G->S);15586(SNP:G->K);15810(SNP:C->Y);28253(SNP:C->Y);28378(SNP:G->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CruiseA-25/2020	MT184912	11083(SNP:G->T);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
2019-nCoV/USA-CruiseA-26/2020	MT184913	11083(SNP:G->T);12513(SNP:C->Y);20988(SNP:T->Y);25587(SNP:C->Y);28367(SNP:C->Y);28916(SNP:G->A);29882(Deletion:AAAAAAAAAAAAAAAAAAAAAA->A)
```

## Contribution


## Citation
Please cite this for 2019 Novel Coronavirus Resource:
```
Zhao WM, Song SH, Chen ML, et al. The 2019 novel coronavirus resource. Yi Chuan. 2020;42(2):212–221. doi:10.16288/j.yczz.20-030 [PMID: 32102777]
```
or BibTeX Format:
```
@article{zhao20202019,
  title={The 2019 novel coronavirus resource.},
  author={Zhao, Wen-Ming and Song, Shu-Hui and Chen, Mei-Li and Zou, Dong and Ma, Li-Na and Ma, Ying-Ke and Li, Ru-Jiao and Hao, Li-Li and Li, Cui-Ping and Tian, Dong-Mei and others},
  journal={Yi chuan= Hereditas},
  volume={42},
  number={2},
  pages={212--221},
  year={2020}
}
```
Please cite this for Network Construction Method:
```
XXX
```



## Contact
If you have any questions, feel free to contact us. XXX@big.ac.cn

## License
MIT...
