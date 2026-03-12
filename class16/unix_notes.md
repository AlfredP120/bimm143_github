## Basic Unix

Some important file system commands include

pwd: Print working directory
ls: List files and folders
cd: Change Directory
mkdir: Make a new directory
rm: Delete files and directories
nano: A very basic text editor that is always available
less: To view/read text files page by page (pager program)

My AWS instance:
ssh -i ~/Downloads/bimm143_alfred.pem ubuntu@ec2-34-216-222-251.us-west-2.compute.amazonaws.com

To copy from my AWS instance
scp -i ~/Downloads/bimm143_alfred.pem ubuntu@ec2-34-216-222-251.us-west-2.compute.amazonaws.com:~/work/results.tsv .

# Class 17 AWS
# ssh -i ~/Downloads/bimm143_alfred.pem ubuntu@ec2-35-93-160-113.us-west-2.compute.amazonaws.com