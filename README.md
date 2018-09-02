#Dockerfiles for webwork2

Collecting docker files and their Git history from webwork2/ using 
	https://github.com/nmoller/webwork2
as the source after a major cleanup.

Cleanup:

cd /tmp
mkdir -p WW-just-dockerfiles/current
cd WW-just-dockerfiles/current

git clone https://github.com/nmoller/webwork2.git
cd webwork2/
git checkout rel-ww2.14
git remote rm origin
git rm -rf bin clients conf courses.dist DATA doc htdocs lib LICENSE logs PG_VERSION README README_js_organization README.md README.md.bak t tmp VERSION .gitignore

git commit -m "Delete everything except docker files"

# Download BFG from https://rtyley.github.io/bfg-repo-cleaner/
# to /tmp

alias bfg="java -jar /tmp/bfg-1.13.0.jar"

bfg --no-blob-protection --delete-folders "{bin,clients,conf,courses.dist,DATA,doc,htdocs,lib,logs,t,tmp}"

bfg --delete-files "{LICENSE,PG_VERSION,README,README_js_organization,README.md,README.md.bak,VERSION}"

git reflog expire --expire=now --all && git gc --prune=now --aggressive

git branch
git branch -D ubc

git tag
git tag -d "2.5.1.1"
git tag -d "2.8"
git tag -d "WeBWorK-2.10"
git tag -d "WeBWorK-2.6"
git tag -d "WeBWorK-2.6+"
git tag -d "WeBWorK-2.7"
git tag -d "WeBWorK-2.7+"
git tag -d "WeBWorK-2.8"
git tag -d "WeBWorK-2.9+"



git filter-branch --prune-empty  -- --all

git filter-branch -f --commit-filter 'git_commit_non_empty_tree "$@"' -- --all

git reflog expire --expire=now --all && git gc --prune=now --aggressive

git log Dockerfile docker-entrypoint.sh docker-compose.yml .dockerignore > ../C-ALL
# Find commits to reuse

git branch

git checkout --orphan master bb0c30ef62f119beb2af2c834bfc5f89d431bc7c

echo "#Dockerfiles for webwork2" > README.md
vim README.md
# Wrote this file - stage 1

git add README.md
git commit -a 



