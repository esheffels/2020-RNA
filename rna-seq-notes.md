Using AI platform notebooks (Jupyter notebook implementation with GCP integration, machine learning tools, and GitHub repository integration

want: total size of data files
export metadata to txt file using cloud console: 
from cloud console:

create folder and text file:

mkdir processing
cd processing
touch /processing/metadata_2020_11_03.txt 

write bucket data folder metadata to text file:

gsutil ls -L gs://sbi-sheffels-e/data** > ~/processing/metadata_2020_11_03.txt

move text file to bucket data folder

gsutil mv metadata_2020_11_03.txt gs://sbi-sheffels-e/data

clean up processing folder (if finished):
cd ..
rmdir processing

In AI Platform notebook:
Install Java
download Java files and upload to bucket
follow instructions:
https://askubuntu.com/questions/56104/how-can-i-install-sun-oracles-proprietary-java-jdk-6-7-8-or-jre

## GitHub
https://cloud.google.com/ai-platform/notebooks/docs/save-to-github
### Set up a GitHub repository in a Notebook instance.
1) Create a GitHub repository on GitHub (use lab organization account).
2) Fork the repository to your personal account for development.
3) In your AI Platform Notebook instance, open a terminal and enter the following commands to configure your Git user name and email. Set your email as private on GitHub and use your GitHub provided email (nnnnnnn+user-name@users.noreply.github.com).
git config --global user.name "user-name"
git config --global user.email "your-email"
4) Go to the repository page in GitHub and copy the repository URL (click the code download button).
5) In your Notebook instance, go to the Git menu and choose Clone a Repository, then enter the repository code. The repository will be added as a new folder.
### Add changes to a GitHub repository
1) Move files into the repository folder, create new files in the folder, or change files already in the folder.
2) Go to the Git tab to the left of interface (diamond with a branched line).
3) Files will automatically be untracked, which means that changes will not be logged in the repository. Checkpoint files and other temporary files should remain untracked. For files that you want to be updated in the repository, hover over the file name and click the plus button. The file will be moved to the staged list, indicating that changes are ready to be pushed to the repository. 
4) Add a summary (mandatory) and description (optional but encouraged) of the changes you have made to the repository files since the last commit. Detailed summaries and descriptions are very helpful when looking back through a project in the future. 
5) Click the Commit button. Changed/new files should be moved to the Staged list.
6) Open a terminal and change the working directory to the repository folder if not there already. 
7) Confirm that your Git user name and email are set correctly. The following commands should print the current user name and email, respectively, if you are unsure. 
git config --global user.name
git config --global user.email
8) Enter the following command and enter your GitHub user name and password when prompted.
git push
9) The staged file list should be empty and the new files/changes should show up in the repository on GitHub, along with the commit notes.