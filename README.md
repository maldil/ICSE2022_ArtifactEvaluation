# Discovering Repetitive Code Changes in Python ML Systems
We made all the tools and data used in the research publicly available in order to claim "Available" and "Reusable" batches.

## About the artifact

We release two tools
* [Py-RefactoringMiner](https://github.com/maldil/RefactoringMiner) - a tool that mines Python refactoring in git commits of Python systems
* [R-CPATMiner](https://github.com/maldil/R-CPATMiner) - a tool that mines fine-grained code change patterns in Python systems
This artifact consists of the open source versions of the tools ([Py-RefactoringMiner](https://github.com/maldil/RefactoringMiner), [R-CPATMiner](https://github.com/maldil/R-CPATMiner)) and a subset of the small sized open-source projects used in the research. We have readily installed two tools on a [Docker container](https://docker-curriculum.com/#what-is-docker-) and included the evaluation subjects for the reviewer’s convenience. The tools' git repositories provide detailed instructions on building and using the tools.

We made two types of large datasets publicly available in https://mlcodepatterns.github.io. These datasets were extracted using the above tools.
* 2,062 instances of validated Python refactoring instances
* 28K fine grained code change patterns discovered in Python ML systems

As the first step, we describe the steps to evaluate the tools (Section 1). We first explored the guidelines to execute the tools in Docker Containers on toy projects which can be done under 30 minutes. In section 2, we described our public datasets. Comprehensive explanation of building the tools and then using it on a  dataset is provided in Section3. 

You could use Mac OS’ CLI, Windows powershell, or Linux terminal to execute the commands. 

## 1. Tool evaluation
### a. Initial setup

**Step 1.1:**  Docker may be downloaded via https://docs.docker.com/get-docker/. To verify that Docker is installed successfully, use the command docker —version from your Terminal. By clicking on the docker icon, you launch the program to proceed.

**Step 1.2**: Open your terminal and go to the folder where you will be saving all of the data and tools. You may make a new folder and then go inside it in your terminal. The command  `pwd` (`cd` in Windows) should be run from the folder. The command should print your folder's absolute path. We will name it `$FOLDER_PATH`.

**Step 1.3**:  [This folder](https://drive.google.com/file/d/1mWy046yjHrywRUf_g_wklwiyGtb5Ggtn/view?usp=sharing) should be downloaded, unzipped, and saved to the `$FOLDER PATH` directory. You should see the following folder in the `$FOLDER_PATH` directory. 

>**Note** - If you have a Windows operating system, the zipped folder will be extracted to another parent directory. Check that the `$FOLDER PATH` contains the following downloaded directory (not the one that you are extracting the zipped folder).

<img src="https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/Atrifact_Folder.png" width="200" height="230" />

This is the folder structure we will use within the Docker containers. The Docker containers are hardcoded to read and write data to these directories. Therefore, preserving this folder structure is critical. The Docker container's binaries will create data in this folder, which the reviewers must examine. Reviewers should be able to see the created data in this folder, and they should be able to do so using their preferred applications. For example, if an HTML file is produced inside this folder, reviewers can access the material using a web browser.


### b. Evaluating R-CPATMiner

**Step 2.1**- To download the required Docker container, execute following command

```docker pull malindadoo1/python-cpatminer:6.0```

**Step 2.2**- To start the container execute following command in your terminal

```docker run -v $FOLDER_PATH/ArtifactEvaluation:/user/local/cpatminer/ArtifactEvaluation -it malindadoo1/python-cpatminer:6.0 /bin/bash```

Again, `$FOLDER_PATH` has to be the absolute folder path of the parent  folder of `ArtifactEvaluation` that you downloaded in step 1.
You will be entered to the interactive mode of the Docker container. Execute the command `ls` and check the folders `ArtifactEvaluation`,  `atomicminer`, and  `changeminer` are available in the current directory (`/user/local/cpatminer`).  

**Note**-  Fine grained pattern generation consists of two steps, i.e.,(1) change graph generation, and (2) code change pattern generation. You can specify the `selected-repos.csv` file in the folder `CPATMiner` shown below to specify the project for change graph generation. Here we have already specified a project that takes only a few minutes for complete analysis. You do not have to change this file unless you want to add more projects there. If you add new projects by editing `selected-repos.csv`, the type information downloaded from our type repository must be placed in the folder `/ArtifactEvaluation/RepoData/TYPE_REPO`. 
If you do not want to alter `selected-repos.csv`, you do not need to do anything because we have already supplied type information for our toy project.

<img src="https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/selected_repos.png" width="200" height="230" />

**Step 2.3** Execute the following command to see if the container is correctly launched.

```python3 test_container.py```

If this command prints the message, **You've done an excellent job mounting the folders** appears after running this command, you've successfully finished step 2.2. You can go to the next step now. If not, make sure the variable `$FOLDER PATH` is set to the absolute path of the download folder's parent folder (go to step 1.3).


**Step 2.4** To run R-CPATMiner and generate patterns in the projects specified in `selected-repos.csv`, execute:

```./test_cpatminer.sh``` 

This shell script consists of the commands that need to 1) generate change graphs generation and 2) pattern generation. You can use `vi test_cpatminer.sh` to view the commands.

**Observation 1** - Change graphs should have been generated inside the folder `$FOLDER_PATH/ArtifactEvaluation/CPATMiner/OutPutChangeGraphs/maldil/MLEditsTest` as below.

<img src="https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/change_graphs.png" width="500" height="150" />


**Observation 2** - Code change patterns should have been created inside the folder `$FOLDER_PATH/ArtifactEvaluation/CPATMiner/Patterns/OutPutChangeGraphs-hybrid/2` in your computer.

<img src="https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/directory_html.png" width="200" height="230" />

Open the html file `directory.html` using any of your browsers. You can see the change patterns that have been generated as below. 

<img src="https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/patterns.png" width="700" height="50" />

A code change pattern is represented by a row in this generated table. The number of code change occurrences per pattern is represented by the column **NumberFound**. Click the hyperlinks in the **Details** column to view each case. It should take you to the page below, which has all of the occurrences for the relevant pattern. To see the actual changes on GitHub, click on the **Link** hyperlinks.

For example, if you click on the hyperlink **location** in the second row, which has the most occurrences, you should see the `html` file below, which illustrates moving from `sum()` to `for loops`.

<img src="https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/pattern.png" width="250" height="450" />

**Step 3.4** Now, you saw how [R-CPATMiner](https://github.com/maldil/R-CPATMiner) mines code change patterns. You can execute exit to terminate the container. You can still access all the generated files in the mounted folder.


### c. Evaluating the RefactoringMiner

**Step 3.1**: To download the docker images, execute the following command in your terminal 

```docker pull malindadoo1/python_refactoring_miner:r11 ```

Once the download is completed, run the command docker images and make sure that the image `python_refactoring_miner` with tag `r11` is available.

**Step 3.2**: To start the docker container in interactive mode, execute the following command in your terminal 

```docker run -v $FOLDER_PATH/ArtifactEvaluation:/user/local/rminer/ArtifactEvaluation -it malindadoo1/python_refactoring_miner:r11 /bin/bash```

Same like in Step 2, You have to update the variable `$FOLDER_PATH` correctly. It should be the absolute path to the parent folder of the downloaded folder `ArtifactEvaluation`. We have to mount it to the docker container. Once you execute the above command you will be entered to the docker container. 

**Step 3.3**- This step is to check whether the container is started correctly. Execute:

```python3 test_container.py ```

If this command prints the message, **You've done an excellent job mounting the folders** appears after running this command, you've successfully finished step 3.2. You can go to the next step now. If not, make sure the variable `$FOLDER PATH` is set to the absolute path of the download folder's parent folder.


**Step 3.4**- Let’s run the refactoring miner and extract some refactorings. First, use the command `pwd` to check whether your current working folder is `/user/local/rminer`. If not, you should first navigate back to the folder `/user/local/rminer`. 
After ensuring that the working directory `is /user/local/rminer`, run the following command.

```java -jar target/python-refactoring-miner-1.0.6.jar -dc``` (Ignore the log4j warnings.)

The `.jar` file is preconfigured to read the file `/ArtifactEvaluation/RefactoringMiner/repo_data.csv` which has the repository and commit hex of the commit that we want to extract refactorings. If you want to add more projects and hex you can edit the file and add more projects and commit hexes. However, you must download inferred type information from the [type repository](https://github.com/mlcodepatterns/PythonTypeInformation) and add it to the subdirectory `TYPE_REPO`, if you wish to analyze more commits and projects than the ones in `repo_data.csv`.


**Step 3.5***- Step 3.4 saves all refactoring data to individual `.json` files in the `$FOLDER PATH/ArtifactEvaluation/RefactoringMiner/Refactoring` folder. Now we must compile all of this information into a single file. To do so, go to the `/user/local/rminer` folder and run the following command.

```python3 conver_to_csv.py ./ArtifactEvaluation/RefactoringMiner/Refactoring/```

**Observation-1**
This will generate the file `$FOLDER_PATH/ArtifactEvaluation/RefactoringMiner/Refactoring/refactoring.csv`. This file is generated in the folder that you downloaded and mounted to the docker container. 

The file `refactoring.csv` contains a summary of all the refactoring of the commits specified in the file `$FOLDER_PATH/ArtifactEvaluation/RefactoringMiner/repo_data.csv`. When you open the refactoring.csv in `Excel` it should look like below. 

<img src="https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/Excel.png" width="550" height="40" />

You can go to each commit URL and check whether the refactoring described in the column Description is available. This file described only a little information. Additional informations are available in the `.json` files in the subdirectories of  `$FOLDER_PATH/ArtifactEvaluation/RefactoringMiner/Refactoring`

**Step 3.6** - Execute `exit` to terminate the container. 

##  2. Public dataset

We present the data which was generated by the above evaluated tools i.e., R-CPATMiner and RefactoringMiner. The dataset is generated by running the tools over 1000 open source machine learning projects. The project list is specified in this [file](https://github.com/maldil/ICSE2022_ArtifactEvaluation/blob/main/Images/selected-repos.csv). Reviewers can regenerate all the data using the above tools. However, we do not expect the reviewers to execute the tools on this dataset because it takes a long time to complete and cannot be completed in less than 30 minutes.


* **Dataset 1:** R-CPATMiner generated 28,323 code change patterns which is publicly available in this link https://mlcodepatterns.github.io/icse_sp8/directory.html.
* **Dataset 2:** We manually analyzed 2,500 most popular code change patterns and presented 22 code change patterns in the paper. The dataset is available in https://mlcodepatterns.github.io/summary_icse/pattern_summary_final_v1.html.
* **Dataset 3:** We manually analysed 2,062 refactoring dataset reported by the RefactoringMiner. We make the manually validated dataset available to the public https://mlcodepatterns.github.io (Item 3).

## 3. Building the tools 

In step 2, we showed you how to use the tools in Docker containers. If the reviewers complete all of the processes at this point, you have successfully executed the tools and verified that they are functional and that the data and tools are publicly accessible. Let's see whether the tools are reusable now.

If reviewers want to build the tools and perform customization or use them as submodules we have given detailed instructions in the tools’ GitHub repositories. Apart from that, the Py-RefactoringMiner is available in the maven repository with the following dependency information. 

* Py-RefactoringMiner = https://github.com/maldil/RefactoringMiner
* R-CPATMiner = https://github.com/maldil/R-CPATMiner

Below is the maven dependency information of the RefactoringMiner. 
```
<dependency>
    <groupId>io.github.maldil</groupId>
    <artifactId>python-refactoring-miner</artifactId>
    <version>1.0.6</version>
</dependency>
```
