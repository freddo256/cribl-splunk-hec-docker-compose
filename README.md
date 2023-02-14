# Cribl - Splunk HEC

This is a sample docker-compose Cribl to Splunk HEC dataflow using a palo-alto datagen.

## Prerequisites
- Docker Desktop 4.16 or newer. (this is required for the Splunk amd64 image to work)

## Setup
1. Clone this repo
2. Set an authentication token in [./splunk_httpinput/local/inputs.conf#L9](./splunk_httpinput/local/inputs.conf#L9) and [./cribl/outputs.yml#L24](./cribl/outputs.yml#L24) for communication between Cribl and Splunk
   - The token has to be formatted like this: `XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX`
3. Set a default splunk password in [./docker-compose.yml#L16](./docker-compose.yml#L16). The default username is `admin`.
4. Run `docker-compose up -d`
5. If Splunk is available on [http://localhost:8000](http://localhost:8000) and Cribl on [http://localhost:9000](http://localhost:9000), data should start flowing to the main index automatically.
   1. The default credentials for Cribl are `admin:admin`
6. The Palo Alto datagen data is now flowing to Splunk HEC in the Splunk container


# Troubleshooting
If the HEC destination does not work in Cribl, and you get a `Sender is blocked` error, you may have to take a look at the SSL settings. Make sure SSL is enabled on the Splunk HEC input and Cribl sends data over https.
