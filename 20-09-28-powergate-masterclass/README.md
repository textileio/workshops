# Powergate Masterclass

Given on line on 28 September 2020. Document below not maintained, always use https://docs.textile.io for the most up-to-date methods and resources.

## Notebooks

`cd` into the `Notebooks` folder and run: `jupyter notebook`

## Preparation

* Install Docker Desktop: https://www.docker.com/products/docker-desktop
* Clone Powergate repo: https://github.com/textileio/powergate/

## Running Powergate Localnet

* Docs: https://docs.textile.io/powergate/localnet/

**change wd**

`cd docker`

**inspect makefile**

`cat Makefile`

**inspect & edit dockerfile**

`cat docker-compose-localnet.yaml`

* Take a look at BIGSECTORS
* Update `POWD_FFSMINERSELECTOR=reputation` in Powergate Environment

**run localnet**

`BIGSECTORS=true make localnet`

versus 

`BIGSECTORS=false make localnet`

## Run Powergate in your CI

**ONLY run localnet**

Two ways:

* js-powergate-client way: https://github.com/textileio/js-powergate-client/blob/master/src/index.spec.ts#L9
* docker image way: https://github.com/orbitdb/orbit-db-powergate-io/blob/master/.circleci/config.yml#L21

## Ready for production?

`make up`

* You will sync the entire chain
and it will take time.
* Most APIs will throw errors until the sync completes

## Install the CLI

Two ways:

* Download & install the latest release: https://github.com/textileio/powergate/releases/latest
* Install from the git repo

`which pow`

`make install`

now, try it again:

`which pow`

By default, the CLI is setup to connect to your running Powergate instance (from steps above).

## Admin CLI Commands

* `pow help`
* `pow miners get`
* `pow asks get`
* `pow net peers`

## Python & CLI Example

**change wd into shell folder**

**Install Pygate**

`pip install pygate_grpc`

**Run notebooks**

`jupyter notebook`

**Setup**

```python
from pygate_grpc.client import PowerGateClient
```

**test connection**

```python
client = PowerGateClient("127.0.0.1:5002")

healthcheck = client.health.check()

print("SUCCESS:")
print(healthcheck)
```

## Create a new FFS

**python**

```python
print("Creating a new FFS:")
ffs = client.ffs.create()
```

**CLI**

```sh
pow ffs create
```

## The storage config

**python**

```python
defaultConfig = client.ffs.default_config(ffs.token)
print(defaultConfig)
```

**CLI**

```sh
pow ffs config default -t <TOKEN>
```

### Understanding the FFS

Docs: https://docs.textile.io/powergate/storageconfig/#storageconfig-details

* Slingshot considerations -- don't edit miners.
* Storage considerations -- avoid Hot or leave hot.

## Introduction to the Shell data

* https://springernature.figshare.com/collections/A_shell_dataset_for_shell_features_extraction_and_recognition/4428335

**View the folder of images**

* Orginal data structure
* Walk through the notebook (share link)
* Creating structure
* Populating index
* Generating default HTML file for viewing & searching

### Stage a file

What happens in staging

* pushed to local IPFS
* available for lotus, but not stored permananetly anywhere yet
* could be skipped with a good IFPS connection to Powergate (e.g. swarm connect).

**python**

```python
from pygate_grpc.ffs import get_file_bytes, bytes_to_chunks

iter = get_file_bytes('structured/images.json')

res = client.ffs.stage(bytes_to_chunks(iter), ffs.token)

print(res)
```

**CLI**

```sh
pow ffs stage structured/images.json -t <TOKEN>
```


### Push a new StorageConfig

What happens in staging

* Storage config will be linked to the CID
* If the config says to store in hot, pow will do it
* If the config says to store in cold, pow will do it.
* Pow will try to follow all the rules as best possible.

**python**

```python
output = client.ffs.push(res.cid, ffs.token)
print(output)

logs = client.ffs.logs(res.cid, ffs.token)
for response in logs:
    print(response)
    if response.log_entry.msg.find("execution finished with status") > -1:
        break
```

**CLI**

```sh
pow ffs config push <CID> -w -t <TOKEN>
```

### Get a file

```sh
pow ffs get <CID> output.json -t <TOKEN>
```

### Show the file over gateway

// Bucket CID

### Stage and push a folder

What happens here?

* Muuuuuch bigger dataset
* Longer 

**python**

```ssh
pow ffs stage ./structured -t <TOKEN>
```

**CLI**

```sh
pow ffs config push <CID> -w -t <TOKEN>
```









