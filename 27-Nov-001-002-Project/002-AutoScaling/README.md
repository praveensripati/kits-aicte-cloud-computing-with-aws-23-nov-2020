# AutoScaling with EC2

1. Create an Launch Template for Ubuntu EC2 with the detailed monitoring enabled under the `Advanced details`. Make sure to select the Keypair and the Security Group which will allow the SSH traffic inbound\
![](images/ec2-detailed-monitoring.png)

1. Under the EC2 Management Console, navigate to `Auto Scaling Groups` and click on `Create Auto Scaling group`.\
![](images/create-auto-scaling-group.png)

1. Give the Auto Scaling Group a name and select the template created in the previous step. Click on `Next`.\
![](images/asg-name-launch-template.png)

1. Under the `Configure settings`, select all the `Subnets`. Click on `Next`.\
![](images/asg-select-subnets.png)

1. Go with the default options for `Configure advanced options`. Click on `Next`.\

1. Under the `Configure group size and scaling policies`, specify the `Group size as below`. Select `None` for `Scaling policies`. Click on `Next`.\
![](images/asg-group-size.png)

1. Click on `Next` under the `Add notifications`.

1. Click on `Next` under the `Add tags`.

1. Review all the details and click on `Create Auto Scaling group`.

1. Under the `Instance management` there should be an EC2 instance as shown below.\
![](images/auto-scaling-instance-1.png)

1. Go to the `Automatic scaling` tab and click on `Add policy`.\
![](images/asg-add-policy.png)

1. Select `Simple scaling` and give the policy a name.\
![](images/policy-name-simple-scaling.png)

1. In the same screen click on `Create a CloudWatch alarm` to open a new IAM tab.

1. Click on `Select metric`. Select `EC2`. Select `By Auto Scaling Group`.

1. For the Auto Scaling Group created earlier, select `CPU Utilization`. Click on `Select metric`.\
![](images/cloudwatch-select-metric.png)

1. Specify the metrics and conditions as shown below. Click on `Next`\
![](images/cloudwatch-metrics.png)
![](images/cloudwatch-conditions.png)

1. Under the `Configure actions` click on `Remove`. Click on `Next`.\
![](images/cloudwatch-remove-notifications.png)

1. Give the Alarm a name and description. Click on `Next`.\
![](images/cloud-watch-alarm-name.png)

1. Click on `Create alarm`. Close the tab.

1. Click on the refresh button and select the `CloudWatch alarm`. Also, specify the action as shown below. Click on `Create`.\
![](images/asg-select-cloudwatch-alarm-and-action.png)

1. The Scaling policy should be created as shown below.\
![](images/final-asg-scaling-policy.png)

1. Grab the `Public IP` of the EC2 instance and connect to it via Putty.

1. Run the below command on the EC2 to increase the CPU utilization.
    >dd if=/dev/urandom | bzip2 -9 >> /dev/null

1. Because of the High CPU on the EC2, another EC2 would be automatically added. The same can be noticed in the Auto Scaling Group.\
![](images/asg-another-ec2-added.png)

1. Delete the Auto Scaling Group and the EC2 instances would be automatically terminated.\
![](images/asg-getting-deleted.png)
![](images/ec2-terminated-automatically.png)