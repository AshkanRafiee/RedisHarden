# Redis Hardening
Redis Hardening Checklist
- [ ] First of all if you are using sensitive data try not to use redis as it's not designed for that!
## OS
- [ ] Set Redis Directory Permissions
    > 700
- [ ] Set Redis Config Permissions
    > 600
- [ ] Create a user just for running Redis!
- [ ] Do not use privileged user to run Redis!
- [ ] Use updated version of Redis!
- [ ] Make sure you have a backup procedure!
- [ ] Store your backups with limited permissions and encrypted!
- [ ] Send and Store your Transaction Logs out of main database path!

## Network
- [ ] Do not allow internet access
- [ ] Define Custom Port (Do not use 6379)
- [ ] Define Whitelist of allowed addresses to access port
- [ ] Active TLS for all types of Connections
- [ ] Deploy Redis Isolated from Web Application and other kind of things including DBS Management Applications (phpRedisAdmin, etc.)
- [ ] Use different DBs for different environments (like dev, stage, etc.)

## Authentication
- [ ] Activate Authetication for all kind of users (Admin, User, ReadOnly, etc.)
    > Config ```requirepass``` and ```requiresalt``` at ```redis.conf```
- [ ] Use Strong Passowrd
    > +32 Chars including Lower, Capital letters and numbers
- [ ] Define Authentication Timeout
    > Config ```authfaillocktime``` at ```redis_common.conf``` with something like ```60``` seconds
- [ ] Define Maximum Failed Authentication
    > Config ```maxauthfailtimes``` at ```redis_common.conf```
- [ ] Define Account Locktime
    > Config ```authfaillocktime``` at ```redis_common.conf```

## Input validation
- [ ] Disable/Rename Dangerous Commands using ```rename-command```
    > ```CONFIG```, ```SHUTDOWN```, ```FLUSHDB```, ```FLUSHALL```, etc.
- [ ] Validate strings obtained from untrusted sources Before composing the body of the Lua script using.
- [ ] Validate Usage of SORT Commands for Injections
    > SORT command is using the qsort algorithm and doesn't use a per-execution pseudo-random seed to the hash function unlike other functions!
