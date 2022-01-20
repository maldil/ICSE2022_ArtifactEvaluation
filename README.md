# Discovering Repetitive Code Changes in Python ML Systems

## About the artifact
We release two tools
* [Py-RefactoringMiner](https://github.com/maldil/RefactoringMiner) - a tool that mines Python refactoring in git commits of Python systems
* [R-CPATMiner](https://github.com/maldil/R-CPATMiner) - a tool that mines fine-grained code change patterns in Python systems
This artifact consists of the open source versions of the tools ([Py-RefactoringMiner](https://github.com/maldil/RefactoringMiner), [R-CPATMiner](https://github.com/maldil/R-CPATMiner)) and a subset of the small sized open-source projects used in the research. We have readily installed two tools on a [Docker container](https://docker-curriculum.com/#what-is-docker-) and included the evaluation subjects for the reviewer’s convenience. The tools' git repositories provide detailed instructions on building and using the tools.

We made two types of large datasets publicly available. These datasets were extracted using the above tools.
* 2,062 instances of validated Python refactoring instances
* 28K fine grained code change patterns discovered in Python ML systems

As the first step, we describe the steps to evaluate the tools (Section 1). We first explored the guidelines to execute the tools in Docker Containers on toy projects which can be done under 30 minutes. In section 2, we described our public datasets. Comprehensive explanation of building the tools and then using it on a  dataset is provided in Section3. 

You could use Mac OS’ CLI, Windows powershell, or Linux terminal to execute the commands. 

## Tool evaluation
### a. Initial setup

**Step 1.1:**  Docker may be downloaded via https://docs.docker.com/get-docker/. To verify that Docker is installed successfully, use the command docker —version from your Terminal. By clicking on the docker icon, you launch the program to proceed.

**Step 1.2**: Open your terminal and go to the folder where you will be saving all of the data and tools. You may make a new folder and then go inside it in your terminal. The command  `pwd` (`cd` in Windows) should be run from the folder. The command should print your folder's absolute path. We will name it `$FOLDER_PATH`.

**Step 1.3**:  [This folder](https://drive.google.com/file/d/1mWy046yjHrywRUf_g_wklwiyGtb5Ggtn/view?usp=sharing) should be downloaded, unzipped, and saved to the `$FOLDER PATH` directory. You should see the following folder in the `$FOLDER_PATH` directory. 

>**Note** - If you have a Windows operating system, the zipped folder will be extracted to another parent directory. Check that the `$FOLDER PATH` contains the following downloaded directory (not the one that you are extracting the zipped folder).




