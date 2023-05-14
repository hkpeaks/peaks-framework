## Introduction
Peaks Consolidation is a personal academic project that aims to provide an innovative framework of ETL expression to simplify processing billions of rows using streaming or in-memory model to accelerate dataframe. The project began on February 18th, 2023 in Hong Kong SAR and aims to achieve real-time processing of up to 10 million rows per second on a single computing device and also saving your investment in cloud computing.

Currently, Peaks Consolidation have been innovating and testing a set of algorithms and data structures to support profound acceleration of the dataframe with limited memory. One of the project’s expected outcomes is to solve the data explosion that came with data capture from IoT devices, ERP, internet and data lake. By using a proper script settings, it can support streaming and in-memory models.

When it comes to data structures, bytearray is one of the most useful and memory-efficient. As for algorithms, parallel streaming for reading/writing files and querying is very powerful and can handle billions of rows even on a desktop PC with only 8 cores and 32GB RAM. The author had conducted some research in bioinformatics and had learned that RNA polymerase is responsible for transcribing DNA into RNA while ribosomes are responsible for translating RNA into proteins. The author was impressed by the high efficiency of protein production from transcription to translation, so the data model of Peaks is somewhat similar to these biological operations.

## Ultra Speed for Query Data from a Billion-Row File & Database

Compared to other expensive consolidation solutions e.g, Oracle HFM, SAP BPC, IBM Cognos Controller and TM1, the rule setting of Peaks Consolidation is exceptionally simple for any user. Additionally, CurrentSetting{} allows you to leverage your computing device to deal with billions of rows of queries at your fingertips, whether it’s a single file or a folder containing many files. It can also provide an interface to support your database. Below is an example of rule setting:-

```
CurrentSetting{StreamMB(1000)Thread(100)}

Select{1000MillionRows.csv | Ledger(L10..L20)Account(15000..16000) ~ Table}

Select{Project(>B25,<B23)}

GroupBy{Ledger, Account, Project, D/C, Currency 
        => Sum(Quantity) Sum(Original Amount) Sum(Base Amount)}

WriteFile{Table | * ~ FilterResults.csv}
```

The entire process running on a desktop PC with 8 cores and 32GB of memory takes only 85 seconds using a file with file size of 67.2GB. We are continuously working to improve the algorithm, resulting in better performance with less resource utilization.

StreamMB(1000) allows you to adjust the partition size of data streaming to fit your hardware configuration. The author found that 1000 (e.g., 1GB) is suitable for their computer with 32GB of memory. 

Thread(100) allows you to maximize the usage of multi-core CPU. The author found that 100 threads is suitable for their computer with 8 cores.

If your file is small e.g. less than 10 million rows, normally it is no need to configure these 2 items.


## Trial Version Is Coming Soon

You can download a free and trial versions of runtime for Windows/Linux with use cases. If you have any problem during your testing of the software, please report us in the issues section.

About monthly or bi-monthly, new commands, enhancements and bug fixs will be added to subsequent trial versions. However, it will not include commands which involve complex implementation. Ready-to-use command scripts with sample data will be included in the distribution. For any reported critical bugs, it will be fixed and published as soon as practical.

The initial version will cover the following command groups and commands:-

| Command Group  | Command                        | Remark                                                 |                  
|----------------|------------------------------- |------------------------------------------------------- |
| CurrentSetting | CurrentSetting                 | adjust the size of the partition of your large file    |
|                |                                | and the number threads to match your data and machine  |
| IO             | ReadFile, WriteFile, SplitFile |                                                        | 
| Unique         | Distinct, GroupBy              |                                                        |
| JoinTable      | BuildKeyValue, JoinKeyValue    | two commands must be configured together               |
| Filter         | Select, SelectUnmatch          |                                                        |
| Append         | Append                         | for row/column with adding value/formula               |

## Peaks Framework and DataFrame
Peaks Consolidation comprises of Peaks framework and dataframe that are currently under active development. 

FRAMEWORK: It is an open-source project that aims to promote an alternative standard of ETL expression. It provides a user-friendly command flow that enables working with Peaks DataFramw and third-party softwares.

DATAFRAME: It is a high-performance calculation engine that can be configured by the framework in either streaming mode or in-memory mode easily. 

RELEASES: It will be provided an all-in-one executable runtime for both Windows and Linux. The gRPC version of Peaks Framework which supports Python/Node.js/Java/Rust/.Net will be available in the next stage.

Both framework and dataframe are written in Golang. Currently, the development and testing environment is using Windows 11 and AMD x86, and will support Linux. Apart from AMD x86, it will also support ARM CPU. For fast-growing RISC V in IoT applications, which is one of considerations.

## File Format
Currently, Peaks Consolidation supports tables in CSV file format only and will support other popular table formats such as XLSX, JSON, PARQUET and FASTA.

XLSX is a popular file format for accounting. It’s likely that Peaks Consolidation will support this format by considering the Excelize library for Golang. 

PARQUET is a format that is built to handle flat columnar storage data formats. It is designed for efficient data storage and retrieval. The format stores data in “row group” blocks that are divided into “column chunks” and then further divided into “data pages” .

FASTA format is a text-based format that supports bioinformatics. It is used for representing either nucleotide sequences or amino acid (protein) sequences. In this format, nucleotides or amino acids are represented using single-letter codes for five nucleobases— adenine (A), cytosine (C), guanine (G), thymine (T), and uracil (U). Unknown bases are represented by the letter N. The human genome is a diploid genome that contains 3.2 billion nucleotides. These nucleotides are packed into 23 pairs of chromosomes.

## Resource Utilization Does Matter
JoinTable is an ETL function that is frequently used. However, it has been reported that JoinTable can be problematic when processing tables with billions of rows. 

Golang is a simple and beautiful programming language that allows JoinTable to implement ultra-performance streaming. For instance, it can process a 67.2GB CSV file and output 91GB. 

According to the Windows Task Manager for many testing results, Peaks Consolidation demonstrates high efficiency in resource utilization during the processing of billions of rows for JoinTable. You can continue to enjoy YouTube during the intensive data processing.

Apart from JoinTable, this url https://youtu.be/9nxIDi2t1Bg is a demo video which apply a query statement "Select{1000MillionRows.csv | Ledger(L10…L15,L50…L55,L82…L88) Account(12222…12888,15555…16888) Project(>B28,<B22) ~ Peaks-Filter1000M.csv}" to select 15,110,000 rows from the 1 billion rows file. The whole processing time is 124 seconds running on a 3-year-old desktop PC with only 32GB RAM. Utilization of memory resources throughout the process is near half. Less resource demanding if comparing a JoinTable test.

## Consolidation Rules for Financial Close and Budgeting

Peaks Consolidation will help with statutory compliance and management ad-hoc reporting for financial consolidation with thousands of business units and legal entities by the following conolidation rules:-

1. Voucher generation e.g. reversal, amortization, acquisition, displosal, fair value adjustment
2. Segmental multi-currency account periodical balance e.g. Yearly, Weekly, Daily
3. Account allocation
4. Account reconciliation
5. Foriegn currency

   a. Revaluation at entity level   
  
   b. Translation at consolidation level  
   
5. Elimination of inter-company transactions
6. Re-alignment of different year-end dates with different consolidation methods

   a. Proportional accounting
  
   b. Equity accounting
   
   c. Full consolidation with calculation of minority interest
   
7. Standardization of dataset

Your dataset can be standardized using a conditional mapping engine that is equipped with effective date of change calculation rules. This engine can help you address your ever-changing incentive plans for different stakeholder management, account allocation, and sharing holdings in investment in subsidiaries, joint ventures, and associates.

The mission of Peaks Consolidation development roadmap is to empower you to achieve advanced accounting automation anywhere, progressing towards real-time accounting automation.

## Software Integration

The author loves using Golang because it is a high-performance programming language with a beautiful syntax design. It is exceptionally easy to learn and has strong support from the community. As a result, the author is considering integrating Peaks Consolidation with other software written in Golang. Below are some of projects why the author finds Golang is very attractive: -

### TiDB
TiDB is a distributed SQL database that supports Hybrid Transactional and Analytical Processing (HTAP) workloads.

### CloudQuery
CloudQuery is a serverless SQL query engine that can be used to query data from various cloud storage services.

### Docker
Docker is a containerization platform and runtime that allows developers to build, package, and deploy applications as containers.

### Kubernetes 
Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

### gRPC
gRPC is a modern open-source high-performance Remote Procedure Call (RPC) framework that can run in any environment. It has an official Go implementation called grpc-go.

Since Golang doesn’t have a hyper-performance dataframe library similar to Polars for Rust, the author was motivated to create a better one for the Golang community.

## About the Author

The author is an experienced accountant and IT professional with over three decades of experience. He qualified as an accountant in 1998 and has worked with some of Hong Kong’s listed companies in various capacities.

From 2006 to 2008, he was an Assistant Chief Accountant at PYI/Paul Y. Group where he managed the daily accounting operations of PYI Group and oversaw the implementation of FlexAccount V10 for two listed companies and their subsidiaries.

From 2008 to 2010, he was an Assistant Finance Manager at Giordano where he conducted user requirement analysis and solution sourcing for automating the consolidated financial statements of the listed company. He recommended FlexSystem to customize its draft ledger and query technology for the financial consolidation needs.

From 2010 to 2020, he worked as a consultant at FlexSystem where he acquired extensive experience with three consolidation software development: FESA Consolidation, LedgerBase and FlexCalc.

He retired at the age of 52 due to the COVID-19 pandemic. He continued to work on two personal visual projects using DotNet and HTML5: youFast Desktop (https://lnkd.in/gGB34cH) and WebNameSQL (https://lnkd.in/gkfREsvK).

In early 2022, he evaluated Rust, Golang and C++ and finished a prototype that migrated the WebNameSQL project from DotNet to Golang in four months. Then he took a break from software development and learnt bioinformatics using Bioconductor and machine learning using TensorFlow and Pytorch.

He is currently working on the cross-platform consolidation project which uses gRPC to support different programming languages such as Rust, Golang, Node.js, DotNet and Python. He is 55 years old but remains young in mindset.

Peaks Consolidation is expected to be his final research and development in consolidation software as its algorithms and data structures have been proven very outstanding. 
