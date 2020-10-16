# Buckets Masterclass

Given on line on 30 September 2020. Document below not maintained, always use https://docs.textile.io for the most up-to-date methods and resources.

## Getting started with the Hub

* Releases https://github.com/textileio/textile/releases/tag/v2.1.0
* or `git clone git@github.com:textileio/textile.git`

**from source**

`cd textile`
`make installs`

**tour cli**

`hub help`


## Data Example

**Run notebooks**

`jupyter notebook`

**Show the source data url**

https://springernature.figshare.com/collections/Ashelldatasetforshellfeaturesextractionandrecognition/4428335

**Show the data transform notebook**

**Show the output folder**

cd into the structured data. and count all files,

`-type f -print | wc -l`

**Show the index.html**

Show data transform example

**Run a local server**

cd into the output folder

`python -m http.server 8000`

## Creating a bucket

docs: https://docs.textile.io/buckets/

cd into our output folder

`hub buck init`

`hub buck push`

What happens? https://blog.textile.io/buckets-diffing-syncing-archiving/

## Working with private buckets

https://hub.textile.io/thread/bafkqvif37deytyf2bz2xih4gzdvsck2upe4th4asbf6qxvty2jzjedy/buckets/bafzbeicflbasceyy6xg7g4b5wstlwntdkfekwemxisrlhqvj2oq2buyely

**Encrypt contents**

**View contents**

**Push read role**

`hub buck roles grant "*" aandara/consociata/10_a.jpg -r reader`

Check out the shared path in the browser

## Archiving a bucket

**help**

`hub buck archive --help`

**default config**

`hub buck archive default-config`

Learn more: https://docs.textile.io/powergate/storageconfig/#storageconfig-details

**info**

`hub buck archive info`

**status**

`hub buck archive status`

### Archive

`hub buck archive`

**Tour through the commands above again with the new archive**

## Buckets online

```sh
hub buck links
```