# van Lon & Holvoet (2015) 
Code and results for demonstration experiment of Rinde R.S. van Lon and Tom Holvoet, Towards systematic evaluation of  multi-agent systems in large scale and dynamic logistics. PRIMA 2015: Principles and Practice of Multi-Agent Systems, (2015).

## Code for generating dataset

```
mvn exec:java -Dexec.mainClass="com.github.rinde.vanlon15prima.GenerateDataset"
```

## Generated dataset files


## Code for performing experiment

```
mvn exec:java -Dexec.mainClass="com.github.rinde.vanlon15prima.PerformExperiment" -Dexec.args="--help"
```

a dot is printed for each simulation that is done. be aware that running the full experiment takes several hours on a 24-core machine.

## Results of experiment



