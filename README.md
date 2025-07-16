# AWS CLOUD COST OPTIMIZATION - IDENTIFYING STALE RESOURCES

1. Launch EC2 Instance

- Go to the EC2 Dashboard

- Create a new instance named test-ec2

- A volume will be automatically attached

  <img width="1871" height="602" alt="Create ec2" src="https://github.com/user-attachments/assets/a5b0fddd-ba3a-45b0-9740-fb46d1139be6" />
  <img width="1901" height="748" alt="volume" src="https://github.com/user-attachments/assets/7c78fcfd-a586-4f45-b302-41e13cda4138" />

2. Create an EBS Snapshot

- Navigate to Snapshots

- Click "Create Snapshot"

- Select the volume attached to test-ec2 (it should appear in the dropdown)

- Add the description: test

- Click "Create snapshot"

<img width="1902" height="646" alt="create snapshot" src="https://github.com/user-attachments/assets/4c4ba784-b9f8-41ab-99ce-c17a7496c584" />


3. Create a Lambda Function

- Go to the Lambda Console

- Create a new function named cost-optimization-ebs-snapshot

- Choose Python 3.10 as the runtime

<img width="1895" height="660" alt="create lambda" src="https://github.com/user-attachments/assets/5d9c5525-68b1-46d5-b106-fc8ff1923ce6" />


4. Add Your Code

- Visit GitHub and copy the function code

- Go back to Lambda > Code tab > Code source section

- Delete the default content in lambda_function.py and paste your code

- Save and Deploy

<img width="1893" height="712" alt="deploy and test" src="https://github.com/user-attachments/assets/a28b8253-f888-4a6d-a0e3-c21bf88b210c" />


5. Test the Function

- Click "Test", name the event test, and click "Test" again

- The test will fail due to missing permissions
  

6. Adjust Function Timeout

- Go to Configuration tab

- Click "General Configuration" > Edit

- Increase timeout to 10 seconds and save
  

7. Attach IAM Policies

- First Policy: Snapshot Permissions

- Go to IAM > Policies > Create Policy

- Choose EC2 service

- Filter actions for:

- DeleteSnapshot

- DescribeSnapshots

- Select "All Resources"

- Name the policy cost-optimization-ebs

- Create policy and attach it to the Lambda role

- Second Policy: Volume and Instance Permissions

- Create another IAM policy

- Select EC2 service

- Add:

- DescribeVolumes

- DescribeInstances

- Name the policy ec2-permissions

- Create and attach this policy to the Lambda role
  
<img width="1895" height="730" alt="create inline policy" src="https://github.com/user-attachments/assets/2e1adaaf-28f6-430d-88c9-ea03c0e25e88" />

<img width="1882" height="673" alt="policies" src="https://github.com/user-attachments/assets/65ae1d3e-15e4-43ce-afe0-b9a5a9c8ce00" />


8. Retest the Function

- Go back to Lambda and click "Test"

- It should now succeed

<img width="1897" height="816" alt="Success" src="https://github.com/user-attachments/assets/deee5020-d3ee-4894-adec-abeabf9f427d" />

- If you delete the Instance it will automatically deletes the volume
- Click the Test again to see if snapshot will be deleted

<img width="1907" height="662" alt="snapshot deleted" src="https://github.com/user-attachments/assets/b262f643-571a-46e0-9006-16ad65b8e2f7" />

