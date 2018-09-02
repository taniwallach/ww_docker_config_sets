# ww_docker_config_sets - sets of Docker files for webwork2

This is a repository for the development and maintenance of sets of Docker 
files for use with the WeBWorK project. We hope to maintain different sets of 
files for different use cases and using different base images, as well as 
instructions on modifying them to fit particular use cases. 

**Note:** the files include a hidden `.dockerignore` file.

The current primary set of files is in the `WW-2.14-ubuntu_16.04` subdirectory
and is for the release candidate of WeBWorK 2.14 and based on the 
Ubuntu 16.04 Docker image. 

Credit for the original sets of Docker files is due to Pan Luo @xcompass 
from the University of British Columbia, which were contributed to 
https://github.com/openwebwork/webwork2 and changes by various others were 
made to those files.

The Git history from the Docker files in the repositories 
  * rel-ww2.14 of https://github.com/openwebwork/webwork2
  * rel-ww2.14 of //github.com/nmoller/webwork2
(as of 2 Sept 2018) was preserved to the best extent I could do.
