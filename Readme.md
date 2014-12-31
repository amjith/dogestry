<div style="float: right"><img src ="http://i.imgur.com/kmS86eG.png" /></div>

# Dogestry

Simple CLI app for storing image on Amazon S3.

## Prerequisites

* Go 1.2 or higher

* Docker

## Usage

### Push

Push the `hipache` image to the S3 bucket `ops-goodies` located in `us-west-2`:
```
dogestry push s3://ops-goodies/?region=us-west-2 hipache
```

### Pull

Pull the `hipache` image and tag from S3 bucket `ops-goodies`:
```
dogestry pull s3://ops-goodies/docker-repo/?region=us-west-2 hipache
```

If you want to pull an image from S3 to multiple hosts, you can use the `-pullhosts` option.
The value for the `-pullhosts` option is a comma-separated list of hosts, in the following
format: `tcp://[host][:port]` or `unix://path`.

The s3 version, with pullhosts:

```
dogestry -pullhosts tcp://host-1:2375,tcp://host-2:2375,tcp://host-3:2375 s3://ops-goodies/docker-repo/ hipache
```

Typical S3 Usage:
```
    export AWS_ACCESS_KEY=ABC
    export AWS_SECRET_KEY=DEF
    export DOCKER_HOST=tcp://localhost:2375
    dogestry push s3://<bucket name>/<path name>/?region=us-east-1 <image name>
    dogestry pull s3://<bucket name>/<path name>/?region=us-east-1 <image name>
```


## Configuration

Configure dogestry with `dogestry.cfg`. By default it's looked for in `./dogestry.cfg`.

Dogestry can often run without a configuration file, but it's there if you need it.

For example, using the config file, you can set up remote aliases for convenience or specifiy s3 credentials.

However, if you're bootstrapping a system, you might rely on IAM instance profiles for credentials and specify the
remote using its full url.


## S3 files layout

Images:
```
images/5d4e24b3d968cc6413a81f6f49566a0db80be401d647ade6d977a9dd9864569f/layer.tar
images/5d4e24b3d968cc6413a81f6f49566a0db80be401d647ade6d977a9dd9864569f/VERSION
images/5d4e24b3d968cc6413a81f6f49566a0db80be401d647ade6d977a9dd9864569f/json
```

Repositories:
```
repositories/myapp/20131210     (content: 5d4e24b3d968cc6413a81f6f49566a0db80be401d647ade6d977a9dd9864569f)
repositories/myapp/latest       (content: 5d4e24b3d968cc6413a81f6f49566a0db80be401d647ade6d977a9dd9864569f)
```


## License

The MIT License (MIT)

Copyright (c) 2014 Blake eLearning

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
