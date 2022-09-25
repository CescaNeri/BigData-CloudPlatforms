# File Formats

The hadoop ecosystem supports several different formats:
- Standard file formats
- Hadoop / BigData-specific formats

Hadoop-specific formats involves several advantages:
- **Serialization**
- **Splittability** (if the file is split into multiple blocks, metadata headers allow to skip unnecessary I/O)
    - Metadata is associated with each single block (the client can access individual blocks)
- **Compression** (if you want to compress the data, you use a compression mechanism that works on a block-level or at a record-level)

There are many file formats - **row-oriented**:
- Sequence files
- Apache thrift (Facebook), Protocol buffers (Google)
    - They both create a notion of schema that has to be used in order to read the data
    - Some code specifies how the data are structured
- Apache Avro 
    - Each file contains its own schema definition (no need to share separately the schema of the file because it is included in the file itself)

## Column-oriented file formats

This formats store data based on columns.
Column-oriented formats are better suited for analytical scenarios. This because in a typical analytical query, you want to take data from a subset of columns and perform analysis.

This format is not ideal for operational purposes (day-to-day operations in a database).

There are several advantaged to column-oriented file formats:
- Better compression (similar values because data is more homogeneous)
- Reduced I/O for analytical queries
- Operate on encoded data

There are many file formats:
- ORC Files
- Apache Parquet (general purpose)

## Parquet

Besides storing data in a column format, it allows to store **nested structures** (like JSON) in a flat format.

 **Data Model**
 Nested attributes that have multiple values.
 - Types:
    - Group
    - Primitive
- Frequency:
    - Required
    - Optional
    - Repeated

![](nested.jpg)

**Unnesting**
Can we store nested data structures in a columnar format?
we need to map the schema to a list of columns in a way that we can write records to flat columns and read them back to their original nested data structure.
- Each value is associated with two integers (repetition level and definition level)
- These integers allow to fully reconstruct the nested structures while still being able to store each primitive separately

When I put values in a column formats, I do not know which value belongs to which record. 
Rebuilding the structure of the rows just by looking at the values cannot be done.
The parquet format allows to reconstruct the message.

![](parquet.jpg)

Parquet uses a definition level that defines the level of definition (0,1,2,3...), dealing with optionality.
This allows you to understand which values exist.
Inside the hierarchy, some fields are mandatory and others are optional. 

**Repetition Level**
The presence of repeated fields requires to store when new lists are starting in a column of values.
Repetition level indicates at which level we have to create a new list for the current value. 

By using these two values (repetition and definition), I am able to fully reconstruct the message.

Repetition and definition level cause overhead (they occupy space).
- The number of bits that has to be used is quite small (1,2,3... the number of levels) and in some case they can be omitted 
- The repetition levels are stored in a column so they can be compressed 

**Parquet file format**
We have a notion of *row group* -> the data are not fully columnar. We do not store all the values of each column continuously.
Usually, we split the file into row groups (horizontal partitioning) and each block of rows store the data in a columnar way. 
- **COlumn chunk** (chunk of the data for a particular column)
All the values of each columns is further subdivided into pages.
The size of the row group is set to the same size of the block (each block corresponds to a row).
**Data page size** -> it can be tuned (smaller or larger) depending on what query we need to issue.






