# Introduction #

The 'maven-external-dependency-plugin' Maven plugin supports the following goals

  * clean-external
  * resolve-external
  * install-external
  * deploy-external

Please see each goal definition below for more details.


&lt;BR&gt;



---


# Goals #

## clean-external ##
This goal will delete any staged artifact files that were previously downloaded.

## resolve-external ##
This goal will attempt to resolve the configured artifact items.  If the artifact can be resolved in the local or one of the configured remote Maven repositories then no further action is taken.  If the artifact can not be resolved in the local or one of the configured remote Maven repositories then this plugin will download the file using the provided 

&lt;BR&gt;

**< downloadUrl >**

&lt;BR&gt;

property and saved it to the configured staging directory.

(_Note: if the artifact item is configured with a MD5 or SHA1 checksum value, this goal will validate the checksum before staging the file.  If the checksum validation fails, the build will be terminated._)

## install-external ##
This goal will first attempt to resolve the configured artifact items in the local Maven repository.  If the artifact item cannot be resolved, then it will look into the staging directory for a downloaded file.  If a staged file for the artifact is found it will install that file into the local Maven repository.

(_Note: if the artifact item is configured with a MD5 or SHA1 checksum value, this goal will validate the checksum before installing the staged the file.  If the checksum validation fails, the build will be terminated._)

## deploy-external ##
This goal will first attempt to resolve the configured artifact items in the local Maven repository.  If the artifact item is found in the local Maven repository it will then deploy that artifact to the configured distribution (remote) repository.


---


# Execution Configuration in POM #

This plugin does not include any default goals that will be executed using any of the standard Maven lifecycle commands.  Instead, you must configure the desired executions section of the plugin to perform the desired goals during the phases you wish.  This was left to be a manually configured task so that the plugin does not make any assumptions about how a user wishes to use it in their project.

Here is an example snippet of the executions configuration.
In this example, a _clean-external_ is performed anytime the standard "clean" phase is invoked.  The _resolve-external_ and _install-external_ goals occur in the "process-resources" phase.  This will force the installation of any unresolved external dependencies prior to the project compile phase and before Maven attempt to resolve all dependencies for compilation.  Finally, the _deploy-external_ goal is invoked with the standard "deploy" phase.  This will force the deployment of all external resources.


```
 <executions>
	 <execution>
		 <id>clean-external-dependencies</id>
		 <phase>clean</phase>
		 <goals>
			 <!-- mvn com.savage7.maven.plugins:maven-external-dependency-plugin:clean-external -->
			 <goal>clean-external</goal>
		 </goals>                     
	 </execution>
	 <execution>
		 <id>resolve-install-external-dependencies</id>
		 <phase>process-resources</phase>
		 <goals>
			 <!-- mvn com.savage7.maven.plugins:maven-external-dependency-plugin:resolve-external -->
			 <goal>resolve-external</goal>

			 <!-- mvn com.savage7.maven.plugins:maven-external-dependency-plugin:install-external -->
			 <goal>install-external</goal>
		 </goals>                     
	 </execution>
	 <execution>
		 <id>deploy-external-dependencies</id>
		 <phase>deploy</phase>
		 <goals>
			 <!-- mvn com.savage7.maven.plugins:maven-external-dependency-plugin:deploy-external -->
			 <goal>deploy-external</goal>
		 </goals>                     
	 </execution>
 </executions>
```


---

Please visit this link for a complete example of a POM file configured for this this plugin:
http://code.google.com/p/maven-external-dependency-plugin/source/browse/trunk/maven-external-dependency-plugin-test/pom.xml