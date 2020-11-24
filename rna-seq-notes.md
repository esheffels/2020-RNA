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