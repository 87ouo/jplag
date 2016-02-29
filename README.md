# Download and Run JPlag
Download a released version - all releases ar single-JAR releases.

Type `java -jar jplag-yourVersion.jar` in a console to see the command line options.

## Example
Assume that we want to check students' solutions that are written in Java 1.7.

Each student solution is in its own directory, say `student1`, `student2`, and so on.
All solutions are in a common directory, say `exercise1`.

To run JPlag, simply type `java -jar jplag-yourVersion.jar -l java17 -r /tmp/jplag_results_exerise1/ -s /path/to/exercise1`

- `-l java17` tells JPlag to use the frontend for Java 1.7
- `-s` tells JPlag to reccurse into subdirectories; as we assume Java projects, we'll very likely encounter subdirectories such as `student1/src/`
- `-r /tmp/jplag_results_exercise1` tells JPlag to store the results in the directory `/tmp/jplag_results_exercise1`

**Note:** You have to specify the language exactly as they are printed by JPlag (running JPlag without command line arguments prints all available languages - and other options).
E.g., if you want to process C++ files, you have specify `-l c/c++` as language option.

# Building JPlag
To build and run a local installation of JPlag, you can use the pom.xml in this directory (aggregator). It builds JPlag and the available frontends. 

To generate single modules run `mvn clean generate-sources package` in the base directory; if you want a single file then run `mvn clean generate-sources assembly:assembly` inside the `jplag` directory. You will find the JARs in the respective `target` directories. If you build a single JAR, it will be generated in `jplag/target`.

## Web Service
Installing, running and maintaining a local web service is not recommended as the web service uses outdated libraries and (really) needs polishing.

If you want to do it anyway: `atujplag` is the client, `webservice` is the - yepp - web service.

# Improving JPlag
We're happy to incorporate all improvements to JPlag into this code base. Feel free to fork the project and send pull requests.

## Adding new languages
Adding a new language frontend is quite simple. Have a look at one of the `jplag.frontend` projects. All you need is a parser for the language (e.g., for ANTLR or for JavaCC) and a few lines of code that sends the tokens (that are generated by the parser) to JPlag.
