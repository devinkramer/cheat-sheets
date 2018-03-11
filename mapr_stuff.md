## Get Resource Manager state
```bash
$ yarn rmadmin -getServiceState rm1
active
$ yarn rmadmin -getServiceState rm2
standby
```

## Storage pools
Display SPs
```bash
/opt/mapr/server/mrconfig sp list -v
```
Remove specific devices
```bash
maprcli disk remove -host `hostname` -disks /dev/sdl,/dev/sdm
```
