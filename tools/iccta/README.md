This directory contains the guidelines to run IccTA taint analysis tool for android.

Here goes the steps to run IccTA.

1) Set up a mysql database. The file "res/schema" should be run in mysql to set up the database.

1.1) create a database: mysql -uusername -ppassword -e 'create database db_name'.

1.2) import the scheme: mysql -uusername -ppassword db_name < res/schema.

2) Next you should run a Epicc or IC3. We opted to run Epicc. 

2.1)  Use runEpicc.sh, but you need to customise the database's HOST, NAME, USERNAME and PASSWORD as well as the ANDROID_JARS.

2.2) Create a directory called "output_iccta" in your working directory. Otherwise, you will get a exception: java.io.FileNotFoundException: output_iccta/[filename].csv (No such file or directory), however, this will not influence the analysis results of Epicc.

2.3) The subdirectory iccProvider/epicc contains the Epicc's jar file and the scripts to run the tool. Before running Epicc, you should set up environment vars. Verify the runEpicc.sh script to make the ajustments.

3)After making the ajustments of the environment vars, one can run Epicc by issuing the command:
./runEpicc.sh path_to_apk

4) Next you can run the IccTA tool. The IccTA jar is located in the "release" directory. 
4.1) java -jar iccta.jar -apkPath path_to_apk -androidJars ..\androidjars\platforms -iccProvider Epicc -nocallbacks -nostatic -intentMatchLevel 3 -nopaths -pathalgo sourceonly

Observation: The above command line allowed to run the tool within minutes. the command:

java -jar iccta.jar -apkPath path_to_apk -androidJars ..\androidjars\platforms -iccProvider Epicc -nocallbacks

took a couple of hours and the computer run out of memory.
