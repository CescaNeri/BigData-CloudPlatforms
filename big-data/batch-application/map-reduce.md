# Map Reduce

It is based, in general, on key-value pairs (data is structured in couples). It is a programming model and an associated implementation for processing and generating large data sets.

How it works:

It is based on typical analytical problems, in which you have large datasets and you want to extract something, you reorganize the data to compute aggregations and generate a final output.

**Map operations and reduce operations**

- MAP takes a function f and applies it to every element in a list
- FOLD iteratively applies a function g to **aggregate** results

## Parallelization

The map operation includes all operations can be parallelized in a straightforward manner, since each functional application happens in isolation.

Reduce operation has more restrictions on data locality.

## MapReduce Program

The map function requires an input (key-value pairs), that are chosen by the programmer.

- Map (k1, v1) -> list(k2, v2)
- Reduce  (k2, list(v2)) -> list(k3, v3)

The output of the map function is a list containing all the values in the row, while the reduce function takes as input a key and the list with all the values associated with that key.

MapReduce program = **job**

- Each job is divided into smaller units called **tasks**
- The tasks are scheduled using YARN and run on nodes in the cluster

## MapReduce Process

1. Input is divided into fixed-size splits
2. A Map task is created for each split
3. The key-value pairs returned by Map tasks are sorted and stored in the local disk
4. Map outputs are sent to the nodes where the Reduce tasks are running
5. The key-value pairs returned by Reduce tasks are written persistently onto the DFS

![](mapreduce.jpg)

## Example - Word COunt

Counting the  number of occurrences for each word in a collection of documents.

**Input:** a repository of documents (each document is a value in the input pairs)

**Map function:** read a document and emit a sequence of key-value pairs

**Shuffle and Sort:** group by key and generate a pairs of the form

**Reduce function:** add up all the values for a given key and emits a pair of the form (w, m)

**Output:** w is a word that appears at least once among all the input documents; m is the total number of occurrences of w among all those documents

```

Map(String docid, String text):
    for each word w in text:
        Emit(w, 1);

Reduce(String term, counts[]):
    int sum = 0;
    for each c in counts:
        sum += c;
    Emit(term, sum);

```

## Map in Java

```
public class WordCountMapperextendsMapper<LongWritable, Text, Text, IntWritable> {
    private static final IntWritableone = newIntWritable(1);
    privateText word = newText();
    public void map(LongWritablekey, Text value, Context context) 
        throwsIOException, InterruptedException{
    String line = value.toString();StringTokenizertokenizer = newStringTokenizer(line);
    while(tokenizer.hasMoreTokens()) {word.set(tokenizer.nextToken());context.write(word, one);
        }
    }
}

```