## EXP.NO:4  RUN A BASIC WORD COUNT MAPREDUCE PROGRAM TO UNDERSTAND THE MAPREDUCE PARADIGM

DATE:

AIM:
To write a basic Word Count program to understand the MapReduce paradigm.

ALGORITHM:
The entire MapReduce program can be divided into three parts:
• Mapper phase code
• Reducer phase code
• Driver code

STEP 1: Mapper code
We create a class `Map` that extends the `Mapper` class defined in the MapReduce framework.
• Input key: offset of each line in the text file (`LongWritable`)
• Input value: each individual line (`Text`)
• Output key: tokenized word (`Text`)
• Output value: hardcoded 1 (`IntWritable`)

STEP 2: Reducer code
We create a class `Reduce` that extends `Reducer`.
• Input key: unique word after sorting and shuffling (`Text`)
• Input value: list of integers corresponding to each key (`IntWritable`)
• Output key: unique word (`Text`)
• Output value: number of occurrences (`IntWritable`)

STEP 3: Driver code
We set the job configuration, specify the mapper and reducer classes, and define input and output paths.

PROGRAM:

```java
import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.input.TextInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.mapreduce.lib.output.TextOutputFormat;

public class WordCount {

    public static class Map extends Mapper<LongWritable, Text, Text, IntWritable> {
        @Override
        public void map(LongWritable key, Text value, Context context)
                throws IOException, InterruptedException {

            String line = value.toString();
            StringTokenizer tokenizer = new StringTokenizer(line);

            while (tokenizer.hasMoreTokens()) {
                String word = tokenizer.nextToken();
                context.write(new Text(word), new IntWritable(1));
            }
        }
    }

    public static class Reduce extends Reducer<Text, IntWritable, Text, IntWritable> {
        @Override
        public void reduce(Text key, Iterable<IntWritable> values, Context context)
                throws IOException, InterruptedException {

            int sum = 0;
            for (IntWritable value : values) {
                sum += value.get();
            }
            context.write(key, new IntWritable(sum));
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "My Word Count Program");

        job.setJarByClass(WordCount.class);
        job.setMapperClass(Map.class);
        job.setReducerClass(Reduce.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);
        job.setInputFormatClass(TextInputFormat.class);
        job.setOutputFormatClass(TextOutputFormat.class);

        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));

        Path outputPath = new Path(args[1]);
        outputPath.getFileSystem(conf).delete(outputPath, true);

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

Run the MapReduce code:
```bash
hadoop jar hadoop-mapreduce-examples.jar wordcount /sample/input /sample/output
```

RESULT:
The basic Word Count program was executed successfully to understand the MapReduce paradigm.
