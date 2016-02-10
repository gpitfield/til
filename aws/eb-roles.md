# EB instance roles

AWS seems to always create roles without adequate permissions when deploying multi-container docker environments.
You need to make sure that the instance role has S3 read access if you're using docker authentication, as well as
access to the Registry Service.