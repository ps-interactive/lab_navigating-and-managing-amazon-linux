# Sample Web Application Lab

This repository is a small simulated web application used for Linux filesystem practice.

Learners will practice:

- Connecting to a Linux EC2 instance with SSH
- Navigating files with absolute and relative paths
- Finding files with `find`
- Searching file contents with `grep`
- Moving and reorganizing files with `mv` and `mkdir`

## Suggested starting directory

After cloning the repo on the EC2 instance:

```bash
cd sample-webapp-lab
```

## Sample tasks

```bash
find . -name "*.html"
grep -R "TODO" .
mkdir backup
mv config backup/
mkdir -p assets/css assets/js assets/images
mv css/* assets/css/
mv js/* assets/js/
mv images/* assets/images/
```
