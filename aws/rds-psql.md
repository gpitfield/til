# RDS PostgreSQL Best Practices

Here's a [quite useful video][1] on optimizing Postgres on RDS. A few suggestions:

* *max_connections*: set this to match what the app actually needs
* *work_mem*: roughly memory/max_connections * haircut (engine default is 1MB)
* *maintenance_work_mem*: 20% of memory (engine default is 16MB!!)
* redshift + postgres_fdw see 9:20 of the video[2]

[1]: https://youtu.be/JWurBmZVgiY
[2]: https://youtu.be/JWurBmZVgiY?t=568