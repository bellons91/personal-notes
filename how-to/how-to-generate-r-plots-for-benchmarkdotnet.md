---
tags: r, benchmarkdotnet, performance, benchmark, dotnet
---

# How to generate R plots for BenchmarkDotNet

[R](https://cran.r-project.org/bin/windows/base/) is a framework to generate graphics and computations.

To use it to generate graphics for BenchmarkDotNet you have to follow these steps:

1. download R from the official website (yes, I know, the website does not look fancy...);
2. install it, and store somewhere the installation path (for me, *C:\Users\d.bellone\AppData\Local\Programs\R\R-4.3.2* );
3. set the enviroment variable on Windows. For some reasons, I couldn't edit the values, so I came up with the next steps;
4. run the benchmarks
5. open the *BenchmarkDotNet.Artifact* folder under the *bin* of your project. For me it's under *\bin\Release\net8.0\BenchmarkDotNet.Artifacts*. You should see some `.log` files;
6. ensure that in the *result* subfolder you have some CSV files and, more important, a file named `BuildPlots.R`;
7. open a terminal in the *results* folder, and run this command: `C:\Users\d.bellone\AppData\Local\Programs\R\R-4.3.2\bin\RScript.exe ./BuildPlots.R`;

Now you should see lots of PNG files with the rendering of the results.

**Who generates those CSV**? If you remember from before, we customized every benchmark with the `[Config(typeof(CsvConfig))]` attribute. This attribute generates both the CSV and the R files, and is defined like this:

```cs
 public class CsvConfig : ManualConfig
 {
     public CsvConfig()
     {
         Add(CsvMeasurementsExporter.Default);
         Add(RPlotExporter.Default);
     }
 }
```
```mermaid```