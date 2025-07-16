# AWS CLOUD COST OPTIMIZATION - IDENTIFYING STALE RESOURCES

1. Launch EC2 Instance

- Go to the EC2 Dashboard

- Create a new instance named test-ec2

- A volume will be automatically attached

2. Create an EBS Snapshot

- Navigate to Snapshots

- Click "Create Snapshot"

- Select the volume attached to test-ec2 (it should appear in the dropdown)

- Add the description: test

- Click "Create snapshot"

3. Create a Lambda Function

- Go to the Lambda Console

- Create a new function named cost-optimization-ebs-snapshot

- Choose Python 3.10 as the runtime

4. Add Your Code

- Visit GitHub and copy the function code

- Go back to Lambda > Code tab > Code source section

- Delete the default content in lambda_function.py and paste your code

- Save and Deploy

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

8. Retest the Function

- Go back to Lambda and click "Test"

- It should now succeed

- If the snapshot is not deleted, test again — the Lambda may have needed updated permissions


