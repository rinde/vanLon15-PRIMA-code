# van Lon & Holvoet (2015) 
Code and results for demonstration experiment of Rinde R.S. van Lon and Tom Holvoet, _Towards systematic evaluation of  multi-agent systems in large scale and dynamic logistics_. PRIMA 2015: Principles and Practice of Multi-Agent Systems, (2015).

## Code for generating dataset

The code for generating the dataset can be found in [DatasetGenerator](src/main/java/com/github/rinde/vanlon15prima/GenerateDataset.java).

To generate the dataset, one can execute (in the project folder):

```shell
mvn exec:java -Dexec.mainClass="com.github.rinde.vanlon15prima.GenerateDataset"
```
This takes about 15 minutes on a 24 core machine. One can also use the generated files as described in the next section.

## Generated dataset files

The generated dataset files can be downloaded here: [![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.27364.svg)](http://dx.doi.org/10.5281/zenodo.27364)

Using RinSim it is possible to run an algorithm on the dataset. Example code that runs a centralized algorithm that randomly assigns parcels to vehicles:

```java
final Experiment.Builder experimentBuilder = Experiment
	.build(Gendreau06ObjectiveFunction.instance())
	.computeLocal()
	.withRandomSeed(123)
	.withThreads(Runtime.getRuntime().availableProcessors())
	.repeat(1)
	.addScenarios(FileProvider.builder()
	    .add(Paths.get("dataset/"))
	    .filter("glob:**[0].scen"))
	.addResultListener(new CommandLineProgress(System.out))
	.usePostProcessor(PostProcessors.statisticsPostProcessor())
	// central: random
	.addConfiguration(
	    Central.solverConfiguration(RandomSolver.supplier()));	    
		    
ExperimentResults er =  experimentBuilder.perform();
```
To retrieve the correct dependencies the following needs to be added in the pom.xml file:
```xml
<properties>
	<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	<rinsim.version>4.0.0</rinsim.version>
</properties>
<build>
	<plugins>
		<plugin>
			<artifactId>maven-compiler-plugin</artifactId>
			<version>2.3.2</version>
			<configuration>
				<source>1.7</source>
				<target>1.7</target>
			</configuration>
		</plugin>
	</plugins>
</build>
	
<dependencies>
	<dependency>
		<groupId>com.github.rinde</groupId>
		<artifactId>rinsim-scenario-util</artifactId>
		<version>${rinsim.version}</version>
	</dependency>
	  <dependency>
        <groupId>com.github.rinde</groupId>
        <artifactId>rinsim-central</artifactId>
        <version>${rinsim.version}</version>
    </dependency>
	<dependency>
        <groupId>com.github.rinde</groupId>
        <artifactId>rinsim-experiment</artifactId>
        <version>${rinsim.version}</version>
    </dependency>
</dependencies>
```

## Code for performing experiment

The code for performing the experiment can be found in [PerformExperiment](src/main/java/com/github/rinde/vanlon15prima/PerformExperiment.java).

To perform the experiment, one can execute (in the project folder):
```shell
mvn exec:java -Dexec.mainClass="com.github.rinde.vanlon15prima.PerformExperiment" -Dexec.args="--help"
```
Note that this command executes only prints the help options that are available, if one wants to run the entire experiment the help option can simply be omitted. Be aware though that running the full experiment takes many hours on a 24-core machine. As a simple progress indicator, a '.' is printed in the command line for each completed simulation.

## Results of experiment

The raw results of the experiment can be found in [results](results/).

## Dependencies:

RinSim: [![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.27360.svg)](http://dx.doi.org/10.5281/zenodo.27360)

RinLog: [![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.27361.svg)](http://dx.doi.org/10.5281/zenodo.27361)

PDPTW Dataset Generator: [![DOI](https://zenodo.org/badge/doi/10.5281/zenodo.27362.svg)](http://dx.doi.org/10.5281/zenodo.27362)
