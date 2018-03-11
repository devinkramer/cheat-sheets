### Syntax Things
```bash
servers.csc.aws1prdcsc{9,1[012]}_csprod_ctgrd_com.cpu_wio
```
this would also work
```bash
servers.csc.aws1prdcsc{9,10,11,12}_csprod_ctgrd_com.cpu_wio
```

### Reformat Legend names to remove FQDN and show last value in legend.
```bash
legendValue(aliasSub(servers.pmz.aws1prdpmz1_webprod_ctgrd_com.mongo.opcounters.*,".*aws1([^_]*).*mongo.opcounters.(\w*)", "\1-\2"),"last")
```

### Reformat Legend names to remove FQDN
```bash
aliasSub(servers.pmz.aws1prdpmz3_webprod_ctgrd_com.mongo.opcounters.*,".*aws1([^_]*).*mongo.opcounters.(\w*)", "\1-\2")
```

### whispher file resizing..
```bash
find fxpp-bid503* -type f -name "dsp_*"  -exec whisper-resize.py {} 60s:2d 15m:31d --nobackup \;
```

### CURL Request
```bash
curl  -gks "https://$GRAPHITE/render?from=-2hours&format=csv&target=ganglia.FOPP-EMX0-LAB1.fopp-emx0000_lab1_fanops_net.load_one“
curl  -gks "https://$GRAPHITE/render?from=-2hours&format=json&target=ganglia.FOPP-EMX0-LAB1.fopp-emx0000_lab1_fanops_net.load_one"
```

### Send a metric to carbon
```bash
echo "local.random.diceroll 4 `date +%s`" | nc  graphite 3003
echo "ganglia.FDTP-NRT0-IAD3.fdtp-nrt0000_iad3_fanops_net.load_five 1 `date +%s`" | nc  graphite 3003
```
