Generating persistence.xml using gradle
This is a sample project that demonstrates how to generate persistence.xml file during gradle build.

Problem
We have a multi module project. Every module consist of two sub modules.  One for entity definitions, and one for bussiness. Every module has a jar file. Application is packaged  as web archive including these jar files.
jar-file tag in persistence.xml accepts only exact file names. No wildcard support for jar-file tag. You should write exact jar file name with version in persistence.xml. 
Every change of one of the modules triggers a persistence.xml update because of version change. Therefore building of application should generate persistence.xml with resolved artifact versions.

Solution
In the project's build.gradle file two tasks are defined. 
'px' task is defined for generating with first level dependencies. The dependencies thah directly listed in build.gradle file.
'allpx' task is defined for generating with all dependencies including the transitive dependencies.

processResources task dependps on px task so that persistence.xml generation is completed before processiong resources.
