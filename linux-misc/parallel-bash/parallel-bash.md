How to run 2 parallel process in a bash script, and wait for them to finish

```
#!/bin/bash
 
function now() {
    local rightnow=`date +%Y/%m/%d_%H:%M:%S`
    echo "$rightnow"
}
 
waitForStuff() {
    ( sleep 5 && echo "done 123 process" & ) | grep -q "done with proc: $1"
    echo "$(now) Background process response: Hey! Process $1 is available"
}
 
echo "$(now) testing 2 processes"
 
waitForStuff ALPHA & ID1=$!
waitForStuff BETA & ID2=$!
 
wait $ID1 && wait $ID2
 
echo "$(now) ID1 is: $ID1, ID2 is: $ID2"
```

