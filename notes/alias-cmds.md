# Alias commands

This note is corresponding for generate certain alias for `.zshrc` file to run, so developers like me who doesn't need to manually type the commands one by one

The common comamnds:

```bash
# commons
alias go-work="cd $HOME/dev/src/github.com/deputyapp/" # go to deputyapp working directory
# docker related
alias docker-clean="docker system prune -f && docker volume prune -f && docker network prune -f && docker image prune -f" # clean up docker resources
# svc-hire commands        
alias go-migrate-hire="TARGET=svc-hire mk aws.migrate.down && TARGET=svc-hire mk aws.migrate.up && TARGET=svc-hire mk aws.seed"
alias docker-svc-hire="TARGET=svc-hire mk compose.up.build AUTH_ENABLED=1"
# svc-hr comamnds
alias go-migrate-hr="mk vendor && TARGET=svc-hr mk aws.migrate.down && TARGET=svc-hr mk aws.migrate.up && TARGET=svc-hr mk aws.seed && TARGET=svc-hr mk data"
alias docker-svc-hr="TARGET=svc-hr mk compose.up.build"
# svc-query command
alias docker-svc-query="TARGET=svc-query mk compose.up.build"
# svc-url commands
alias go-migrate-url="TARGET=svc-url mk mysql.migrate"
alias docker-svc-url="TARGET=svc-url AUTH_ENABLED=1 mk compose.up.build"
# svc-dir command
alias svc-dir-combo="TARGET=svc-dir mk aws.migrate.down && TARGET=svc-dir mk aws.migrate.up && TARGET=svc-dir mk compose.up.build"
```
