# Details #

If you need to resolve, install, and deploy an artifact that is located inside a compressed ZIP file then specify the ZIP file as the download URL and then include the **< extractFile >** property on the **< artifactItem >**.


&lt;BR&gt;




&lt;BR&gt;


**NOTE:**


&lt;BR&gt;


> _As of 0.5-SNAPSHOT, these additional compression formats are supported:  bzip2, dir, gzip, tar, tgz, tar.gz, tbz2, tar.bz2_


&lt;BR&gt;




&lt;BR&gt;


The **< extractFile >** property should be the name of the file (_exact match, case-sensitive_) inside the ZIP file.  If the file to extract is nested inside one or more folders in the ZIP file, then specify the full path and file name. (ie. root/parent/file.ext)


&lt;BR&gt;




&lt;BR&gt;


See the artifact item example below:
```

<!-- HERE IS AN EXAMPLE OF AN ARTIFACT 
     EXTRACTED FROM A ZIP FILE -->
<artifactItem>
	<groupId>com.google.code</groupId>
	<artifactId>tweener</artifactId>
	<version>1.33.74</version>
	<packaging>swc</packaging>
	<downloadUrl>
	   http://tweener.googlecode.com/files/tweener_1_33_74_as3_swc.zip
	</downloadUrl>                        
	<extractFile>tweener.swc</extractFile>                        
</artifactItem>

```



&lt;BR&gt;




&lt;BR&gt;



(..as of version 0.3)

&lt;BR&gt;


If you wish to verify the checksum on an extracted file, please use the **< extractFileChecksum >** property to specify the checksum on the extracted file as the **< checksum >** property will only apply to the download file, not the extracted file.



&lt;BR&gt;


See the artifact item example below that has a checksum defined for the download file and an extractFileChecksum defined for the extracted file:
```

<!-- DIFFERENT CHECKSUMS FOR DOWNLOAD FILE AND EXTRACTED FILE -->
<artifactItem>
    <groupId>de.innosystec</groupId>
    <artifactId>java-unrar</artifactId>
    <version>0.3</version>
    <packaging>jar</packaging>
    <downloadUrl>
         http://github.com/downloads/edmund-wagner/junrar/java-unrar-{version}.zip
    </downloadUrl>
    <checksum>530351609180152cff40fa1c79a28193185aba83</checksum> <!-- this checksum is applied to the download file -->
    <install>true</install>
    <force>false</force>
    <extractFile>java-unrar/java-unrar-{version}.jar</extractFile>							    
    <extractFileChecksum>bce51f76274c41ddac3ca8e99378ff2893108049</extractFileChecksum>  <!-- this checksum is applied to the extracted file -->
</artifactItem>

```


&lt;BR&gt;



---


Please visit this link for a complete example of a POM file configured for this this plugin: 

&lt;BR&gt;


http://code.google.com/p/maven-external-dependency-plugin/source/browse/trunk/maven-external-dependency-plugin-test/pom.xml