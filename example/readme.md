# Grafana dashboards with Influx DB and docker compose

This example demonstrates how to quickly set up a demo environment with Grafana 9.5 and InfluxDB 2.7 using docker compose.

## Give it a try!
Navigate to `./example` and type
```
docker-compose up -d
```

Go to http://localhost:8086/ to check if InfluxDB has started and was configured correctly. Use `superuser` and `Passw0rd!`to log in. You should see the organization `MyOrg` (unless you have changed that in the docker-compose file) and a bucket named `NBomber`

Next, go to http://localhost:3000 to log in into Grafana. The initial user-name/password is `admin` / `admin`.  

The data source and the dashboards are automatically provisioned and should work out of the box.

## Warning
**Do not use this setup in a production environment!**  
At the very least, change the passwords and the InfluxDB token to something unique!  
Better yet, create an InfluxDB token with fewer privileges (e.g. read-only) and use this token for the Grafana data source.

## Sending data from NBomber tests
In order to send data from you NBomber tests to InfluxDB, use the following settings in `infra-config.yaml`

```json
{
  "InfluxDBSink": {
    "Url": "http://localhost:8086?org=MyOrg&bucket=NBomber",
    "Token": "N3Z_uUDSQ61qVp93K5dNzH3rbNcKxtphDLrjfS_DcX2cdTr3nR2pOlixGCx6HQ8VI66nqnyztOlPFoWFXoe62Q==",
    "CustomTags": [
      {
        "Key": "environment",
        "Value": "linux"
      }
    ]
  }
}
```