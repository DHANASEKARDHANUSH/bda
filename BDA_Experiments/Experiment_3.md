## EXP.NO:3  IMPLEMENTATION OF MATRIX MULTIPLICATION WITH HADOOP MAPREDUCE

DATE:

AIM:
To write a MapReduce program that implements matrix multiplication.

ALGORITHM:
We assume that the input matrices are already stored in HDFS in a suitable format such as CSV or TSV, where each row represents a matrix element. The matrices are compatible for multiplication (the number of columns in the first matrix equals the number of rows in the second matrix).

STEP 1: Mapper
The mapper takes the input matrices and emits key-value pairs for each element in the result matrix. The key is the (row, column) index of the result element, and the value is the corresponding element value.

STEP 2: Reducer
The reducer receives the key-value pairs emitted by the mapper and calculates the partial sum for each element in the result matrix.

STEP 3: Main Driver
The main driver class sets up the Hadoop job configuration and specifies the input and output paths for the matrices.

STEP 4: Running the job
To run the MapReduce job, package the classes into a JAR file and then submit it to Hadoop using the `hadoop jar` command.

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

public class MatrixMultiplicationDriver {

    public static class MatrixMultiplicationMapper
            extends Mapper<LongWritable, Text, Text, IntWritable> {

        @Override
        protected void map(LongWritable key, Text value, Context context)
                throws IOException, InterruptedException {

            String[] elements = value.toString().split(",");
            int row = Integer.parseInt(elements[0]);
            int col = Integer.parseInt(elements[1]);
            int val = Integer.parseInt(elements[2]);

            context.write(new Text(row + "," + col), new IntWritable(val));
        }
    }

    public static class MatrixMultiplicationReducer
            extends Reducer<Text, IntWritable, Text, IntWritable> {

        @Override
        protected void reduce(Text key, Iterable<IntWritable> values, Context context)
                throws IOException, InterruptedException {

            int result = 0;
            for (IntWritable value : values) {
                result += value.get();
            }

            context.write(key, new IntWritable(result));
        }
    }

    public static void main(String[] args) throws Exception {
        Configuration conf = new Configuration();
        Job job = Job.getInstance(conf, "Matrix Multiplication");

        job.setJarByClass(MatrixMultiplicationDriver.class);
        job.setMapperClass(MatrixMultiplicationMapper.class);
        job.setReducerClass(MatrixMultiplicationReducer.class);
        job.setInputFormatClass(TextInputFormat.class);
        job.setOutputFormatClass(TextOutputFormat.class);
        job.setOutputKeyClass(Text.class);
        job.setOutputValueClass(IntWritable.class);

        FileInputFormat.addInputPath(job, new Path(args[0]));
        FileOutputFormat.setOutputPath(job, new Path(args[1]));

        System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

Run the program:
```bash
hadoop jar matrixmultiplication.jar MatrixMultiplicationDriver <input_path> <output_path>
```

RESULT:
Thus, the matrix multiplication program using Hadoop MapReduce was implemented successfully.
