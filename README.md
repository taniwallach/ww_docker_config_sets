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

git rm -rf .gitignore 

git add README.md
git commit -a 

vim README.md
# Wrote this file - stage 2

git commit -a  


# Starting stage 2 - cherry-picking the docker commits:

git cherry-pick -e 0b708baa7e9d0815a4975071723b2c25e99d7265
git cherry-pick -e 2e599f33598eb8bccee7887c3e4d5e1782e9fc3e
git cherry-pick -e 98228a5a6fe9e80774d7856bfb0293b38e966f97
git cherry-pick -e 7c39bbd6aa296328b1eee515ed7cedad5ef7609d
git cherry-pick -e 8098fc1f2d6fd916ac8ca320ce8d0fd93e753dbf
git cherry-pick -e d9a86604ed9b00e1df34a25cc735abe43d4e81d2
git cherry-pick -e d7c6953b156a28389c64249ad44586034f93ab6b
git cherry-pick -e 90d568e58cb538d9dc00645f4ad1695bc90c1772
git cherry-pick -e fab202c64de0c8c2b084da092e06c8a990723e02
git cherry-pick -e f5bd4f8547f17118182df4cb91528743824c2199
git cherry-pick -e a9aede2576dfd01861d06d436fdb0a1362c467a1
git cherry-pick -e 7644e9d2b37594cbc99d7e54890d8b9aa0288e33
git cherry-pick -e 93ec7b0ba3611cfd6d5be901af4580fc19bbff61


