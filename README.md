## dbt-performance

Benchmarking dbt in docker containers. See [stats.ipynb](stats.ipynb) for results.

### Requirements

Docker.

### Steps

1. Build our dbt image.

```
docker build -t dbt-rpc . -f Dockerfile.1.3
docker build -t dbt-app .
```

2. Install dependencies.

```
pip install -r requirements.txt
```

3. Run a local Postgres instance.

I used dbt-core's setup [here](https://github.com/dbt-labs/dbt-core/blob/main/CONTRIBUTING.md#initial-setup). The [`profiles.yml`](profiles.yml) file here which we copy over into our image includes the config values that are consistent with connecting to dbt-core's local postgres setup.

4. Run our notebook.

See [stats.ipynb](stats.ipynb).

### Note

We're making use of dbt-core's performance project as the baseline so it's been added as a submodule here.

```sh
git clone https://github.com/jeremyyeo/dbt-performance.git
git submodule init
cp -R dbt-core/performance/projects/01_2000_simple_models .
```

We've also commited the `01_2000_simple_models` project straight into this repository so we can use it in dbt Cloud as well.

### System specs

```
$ system_profiler SPHardwareDataType

Hardware:

    Hardware Overview:

      Model Name: MacBook Pro
      Model Identifier: MacBookPro16,2
      Processor Name: Quad-Core Intel Core i5
      Processor Speed: 2 GHz
      Number of Processors: 1
      Total Number of Cores: 4
      L2 Cache: 1 MB
      L3 Cache: 3 MB
      Hyper-Threading Technology: Enabled
      Memory: 16 GB
      System Firmware Version: 1715.60.5.0.0 (iBridge: 19.16.10647.0.0,0)
      OS Loader Version: 540.60.2~89
      Activation Lock Status: Disabled
```

![](docker-resources.png)
