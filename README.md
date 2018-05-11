# terraform-aws-rds-cluster [![Build Status](https://travis-ci.org/cloudposse/terraform-aws-rds-cluster.svg?branch=master)](https://travis-ci.org/cloudposse/terraform-aws-rds-cluster)

<!---
  --- This file was automatically generated by the `build-harness`
  --- Make changes instead to `.README.md` and rebuild.
  --->

Terraform module to provision an [`RDS Aurora`](https://aws.amazon.com/rds/aurora) cluster for MySQL or Postgres.


## Usage

Basic [example](examples/basic)

```hcl
module "rds_cluster_aurora_postgres" {
  source             = "git::https://github.com/cloudposse/terraform-aws-rds-cluster.git?ref=master"
  engine             = "aurora-postgresql"
  cluster_size       = "2"
  namespace          = "cp"
  stage              = "dev"
  name               = "db"
  admin_user         = "admin"
  admin_password     = "Test123"
  db_name            = "dbname"
  instance_type      = "db.r4.large"
  vpc_id             = "vpc-xxxxxxx"
  availability_zones = ["us-east-1a", "us-east-1b"]
  security_groups    = ["sg-0a6d5a3a"]
  subnets            = ["subnet-8b03333", "subnet-8b0772a3"]
  zone_id            = "xxxxxxxx"
}
```

With [cluster parameters](examples/with_cluster_parameters)

```hcl
module "rds_cluster_aurora_mysql" {
  source             = "git::https://github.com/cloudposse/terraform-aws-rds-cluster.git?ref=master"
  engine             = "aurora"
  cluster_size       = "2"
  namespace          = "cp"
  stage              = "dev"
  name               = "db"
  admin_user         = "admin"
  admin_password     = "Test123"
  db_name            = "dbname"
  instance_type      = "db.t2.small"
  vpc_id             = "vpc-xxxxxxx"
  availability_zones = ["us-east-1a", "us-east-1b"]
  security_groups    = ["sg-0a6d5a3a"]
  subnets            = ["subnet-8b03333", "subnet-8b0772a3"]
  zone_id            = "xxxxxxxx"

  cluster_parameters = [
    {
      name  = "character_set_client"
      value = "utf8"
    },
    {
      name  = "character_set_connection"
      value = "utf8"
    },
    {
      name  = "character_set_database"
      value = "utf8"
    },
    {
      name  = "character_set_results"
      value = "utf8"
    },
    {
      name  = "character_set_server"
      value = "utf8"
    },
    {
      name  = "collation_connection"
      value = "uft8_bin"
    },
    {
      name  = "collation_server"
      value = "uft8_bin"
    },
    {
      name         = "lower_case_table_names"
      value        = "1"
      apply_method = "pending-reboot"
    },
    {
      name         = "skip-character-set-client-handshake"
      value        = "1"
      apply_method = "pending-reboot"
    },
  ]
}
``` 

## Input

<!--------------------------------REQUIRE POSTPROCESSING-------------------------------->
|  Name |  Default  |  Description  |
|:------|:---------:|:--------------:|
| admin_password |__REQUIRED__ |(Required unless a snapshot_identifier is provided) Password for the master DB user|
| admin_user |"admin" |(Required unless a snapshot_identifier is provided) Username for the master DB user|
| allowed_cidr_blocks |[] |List of CIDR blocks allowed to access|
| attributes |[] |Additional attributes (e.g. `policy` or `role`)|
| availability_zones |__REQUIRED__ |List of Availability Zones that instances in the DB cluster can be created in|
| backup_window |"07:00-09:00" |Daily time range during which the backups happen|
| cluster_family |"aurora5.6" |The family of the DB cluster parameter group|
| cluster_parameters |[] |List of DB parameters to apply|
| cluster_size |"2" |Number of DB instances to create in the cluster|
| db_name |__REQUIRED__ |Database name|
| db_port |"3306" |Database port|
| delimiter |"-" |Delimiter to be used between `name`, `namespace`, `stage` and `attributes`|
| enabled |"true" |Set to false to prevent the module from creating any resources|
| engine |"aurora" |The name of the database engine to be used for this DB cluster. Valid values: `aurora`, `aurora-postgresql`|
| engine_version |"" |The version number of the database engine to use|
| instance_type |"db.t2.small" |Instance type to use|
| maintenance_window |"wed:03:00-wed:04:00" |Weekly time range during which system maintenance can occur, in UTC|
| name |__REQUIRED__ |Name of the application|
| namespace |__REQUIRED__ |Namespace (e.g. `cp` or `cloudposse`)|
| retention_period |"5" |Number of days to retain backups for|
| security_groups |__REQUIRED__ |List of security groups to be allowed to connect to the DB instance|
| snapshot_identifier |"" |Specifies whether or not to create this cluster from a snapshot|
| stage |__REQUIRED__ |Stage (e.g. `prod`, `dev`, `staging`)|
| subnets |__REQUIRED__ |List of VPC subnet IDs|
| tags |{} |Additional tags (e.g. map(`BusinessUnit`,`XYZ`)|
| vpc_id |__REQUIRED__ |VPC ID to create the cluster in (e.g. `vpc-a22222ee`)|
| zone_id |__REQUIRED__ |Route53 parent zone ID. The module will create sub-domain DNS records in the parent zone for the DB master and replicas|

## Output

<!--------------------------------REQUIRE POSTPROCESSING-------------------------------->
|  Name | Description  |
|:------|:------------:|
| cluster_name | Cluster Identifier  |
| master_host | DB Master hostname  |
| name | Database name  |
| password | Password for the master DB user  |
| replicas_host | Replicas hostname  |
| user | Username for the master DB user  |

## Help

**Got a question?**

File a GitHub [issue](https://github.com/cloudposse/terraform-aws-rds-cluster/issues), send us an [email](mailto:hello@cloudposse.com) or reach out to us on [Gitter](https://gitter.im/cloudposse/).


## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/cloudposse/terraform-aws-rds-cluster/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing `terraform-aws-rds-cluster`, we would love to hear from you! Shoot us an [email](mailto:hello@cloudposse.com).

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull request** so that we can review your changes

**NOTE:** Be sure to merge the latest from "upstream" before making a pull request!


## License

[APACHE 2.0](LICENSE) © 2017-2018 [Cloud Posse, LLC](https://cloudposse.com)

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.


## About

`terraform-aws-rds-cluster` is maintained and funded by [Cloud Posse, LLC][website].

![Cloud Posse](https://cloudposse.com/logo-300x69.png)


Like it? Please let us know at <hello@cloudposse.com>

We love [Open Source Software](https://github.com/cloudposse/)!

See [our other projects][community]
or [hire us][hire] to help build your next cloud platform.

  [website]: https://cloudposse.com/
  [community]: https://github.com/cloudposse/
  [hire]: https://cloudposse.com/contact/


## Contributors

| [![Erik Osterman][erik_img]][erik_web]<br/>[Erik Osterman][erik_web] | [![Andriy Knysh][andriy_img]][andriy_web]<br/>[Andriy Knysh][andriy_web] |[![Igor Rodionov][igor_img]][igor_web]<br/>[Igor Rodionov][igor_img]
|-------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------|

[erik_img]: http://s.gravatar.com/avatar/88c480d4f73b813904e00a5695a454cb?s=144
[erik_web]: https://github.com/osterman/
[andriy_img]: https://avatars0.githubusercontent.com/u/7356997?v=4&u=ed9ce1c9151d552d985bdf5546772e14ef7ab617&s=144
[andriy_web]: https://github.com/aknysh/
[igor_img]: http://s.gravatar.com/avatar/bc70834d32ed4517568a1feb0b9be7e2?s=144
[igor_web]: https://github.com/goruha/
