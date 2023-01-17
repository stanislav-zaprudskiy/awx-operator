For local scripts debugging and development the following commands could be
used:

```console
temp_dir=$(mktemp -d) \
&& export \
  PRE_STOP_RECHECK_SLEEP=1 \
  PRE_STOP_HANDLER_SLEEP=30 \
  PRE_STOP_HANDLER="bash -c \"FOO=bar $PWD/roles/installer/files/pre-stop/termination-handler\"" \
  PRE_STOP_MARKER_FILE=$temp_dir/.termination_marker \
  PRE_STOP_HEARTBEAT_FILE=$temp_dir/.heartbeat \
  PRE_STOP_BAILOUT_FILE=$temp_dir/.bailout \
  PRE_STOP_STDOUT=/dev/stdout \
  PRE_STOP_STDERR=/dev/stderr; \
{ ./roles/installer/files/pre-stop/termination-master & }; \
./roles/installer/files/pre-stop/termination-waiter
```
