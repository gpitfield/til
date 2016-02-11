# EB instance roles

##### Source: `pain and suffering`

AWS seems to always create roles without adequate permissions when deploying multi-container docker environments. This
may well also be the case when using the Elastic Container Service, though I haven't checked.

By default EB creates two roles, the `aws-elasticbeanstalk-ec2-role` and the `aws-elasticbeanstalk-service-role`, with
a set of default permissions. You may need to add additional permissions to the `aws-elasticbeanstalk-ec2-role` role as follows:
* `ec2-role` needs container service privileges, along the lines of

        ```json
        {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "ecs:StartTask",
                        "ecs:StopTask",
                        "ecs:RegisterContainerInstance",
                        "ecs:DeregisterContainerInstance",
                        "ecs:DescribeContainerInstances",
                        "ecs:DiscoverPollEndpoint",
                        "ecs:Submit*",
                        "ecs:Poll",
                        "ecs:StartTelemetrySession"
                    ],
                    "Resource": [
                        "*"
                    ]
                },
                {
                    "Effect": "Allow",
                    "Action": "s3:PutObject",
                    "Resource": "arn:aws:s3:::elasticbeanstalk-*/resources/environments/logs/*"
                }
            ]
        }
        ```

 Full disclosure: I have not verified whether **all** of those privileges or only a subset are required.
* If you're using private docker repos and need to authenticate, e.g. to docker, and have stored your credentials in S3 then 
`ec2-role` needs S3ReadAccess.
* Finally, if you want to read instance tags, `ec2-role` also needs EC2ReadOnlyAccess or higher.