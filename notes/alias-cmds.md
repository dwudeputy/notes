# Alias commands

This note is corresponding for generate certain alias for `.zshrc` file to run, so developers like me who doesn't need to manually type the commands one by one

The common comamnds:

```bash
1. alias go-work="cd $HOME/dev/src/github.com/deputyapp/" # go to deputyapp working directory
2. alias docker-clean="docker system prune -f && docker volume prune -f && docker network prune -f && docker image prune -f" # clean up docker resources
3. alias go-migrate-hire="TARGET=svc-hire mk aws.migrate.down && TARGET=svc-hire mk aws.migrate.up && TARGET=svc-hire mk aws.seed"
4. 
```