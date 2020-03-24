# Kibana Dashboard

Contains the terraform configuration files to setup the Elasticsearch along with Kibana Dashboard

## Configuration

First create a file with name `terraform.tfvars` this file will store the sensive variables and useful variables (this file isn't versionated)

```bash
# Stage to deploy
stage = ""

# Your AWS profile configuration on credentials file
profile = ""

# Region to deploy
region = ""

# VPC to deploy
vpc_id     = ""

# Elasticseach domain
domain     = ""

# Subnet used to access
subnet_ids = [""]

# Key name to configure the proxy machine
key_name   = "somekeyname"
```

## Building the infra

```bash
# On terminal
terraform init

# Then apply the configuration and confirm if ok
terraform apply
```

## Destroying the infra

```bash
# If you want to destroy everything
terraform destroy
```

## Proxy

The Elastic search access is only allowed inside the the VPC network, in order to access the `Elasticsearch and Kibana` you should create an `SSH Tunel`, the example below will allow to access `Kibana` on `https://localhost:8080/_plugin/kibana`

```bash
export ELASTICSEARCH_ENDPOINT=""
export PROXY_ENDPOINT=""

ssh -N -L 8080:$ELASTICSEARCH_ENDPOINT:443 ubuntu@$PROXY_ENDPOINT
```

> In order to create the SSH Tunnel properly the user should have access to the proxy machine via SSH, so make sure that the port 22 is available for your IP also make sure that your user is allowed on `~/.ssh/authorized_keys` on the proxy instance

## Redirecting Cloudwatch logs to Kibana

In order to stream Cloudwatch logs to Elasticsearch/Kibana you have to create a Lambda function that redirects the logs to the ES instance, luckuly AWS already does that easily with few clicks, just follow the tutorial on https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/CWL_ES_Stream.html

## Authors

* **Rodrigo Serviuc Pavezi** - *Initial work* - [rodrigopavezi](https://gitlab.com/rodrigopavezi)
* **Eduardo Nunes Pereira** - [eduardonunesp](https://gitlab.com/eduardonunesp)
* **Arya Soltanieh** - [lostcodingsomewhere](https://gitlab.com/lostcodingsomewhere)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details





