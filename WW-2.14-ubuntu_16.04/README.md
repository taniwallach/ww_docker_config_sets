# Files for WW+PG 2.14 based on the ubuntu:16.04 base image

**Note:** the files include a hidden `.dockerignore` file.

## Install procedure:

1. Create a new working directory. Example
```
mkdir /data2/webwork_docker_test_new_DF
cd /data2/webwork_docker_test_new_DF
```

2. Clean out your docker from old images and "stages"
```
docker system prune -a
```
* Note: A less drastic cleaning may suffice.

3. Download clean copies of the git repositories, forcing settings
to avoid problems on Windows machines:
```
git clone https://github.com/openwebwork/webwork2 -c core.autocrlf=false -c  core.symlinks=true
git clone https://github.com/taniwallach/ww_docker_config_sets.git -c core.autocrlf=false -c  core.symlinks=true
```

Note: **Optional** If you will later want to core PG code development you may also want to run 
```
git clone https://github.com/openwebwork/pg -c core.autocrlf=false -c  core.symlinks=true
```

4. Change to the 2.14 release of webwork2 and **then** copy in the docker files from the special repository.

```
cd webwork2
git checkout -b rel-2.14 origin/rel-ww2.14
rm -f PG_VERSION    # will replace symlink by a file in next step
cp -af ../ww_docker_config_sets/WW-2.14-ubuntu_16.04/* .
cp -af ../ww_docker_config_sets/WW-2.14-ubuntu_16.04/.dockerignore .
```

5. Fix a bug which interferes with MathJax working, if it has not yet been 
fixed in the rel-2.14 branch.
```
vim conf/localOverrides.conf.dist
```
  * Edit the (active) line which sets $webworkURLs{MathJax} and remove
    `$server_root_url/` from the start of the value, so that the value
    will now start with `$webworkURLs{htdocs}/` (as is the case in
    `conf/defaults.config`    
  * **If you already have** a `vim conf/localOverrides.conf` file (which would not be the case if following this procedure exactly) edit the line in that file **also**.

6. Try to build and start the Docker container: `docker-compose up`

## Successfully tested on:

* Debian 9 with Docker CE (by @taniwallach)
* Windows 10 with Docker CE for Windows (by @taniwallach)
* MacOS X with Docker CR (by @mgage)

## Issues reported on:

* @mgage reported that he had issues when he tried a Docker build after pulling the files into a priorly used webwork2 directory, but that things were fine on a cleanly cloned local repository. 

                                                      
