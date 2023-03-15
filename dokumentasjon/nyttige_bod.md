# Nyttige bod for terminalar
Du kan lese [ordliste her](ordliste.md).

## Git
### PowerShell
#### Finne hovudgreina av depotet du står i
```ps
git remote show origin | ForEach-Object { $_.Trim() } | Where-Object { $_ -match "HEAD branch:" } | ForEach-Object { $_ -replace "HEAD branch:", '' }
```

#### Slette alle avgreiningar frå hovudgreina som er samenslått med hovudgreina.
```ps
git branch | ForEach-Object { $_.Trim() } | Where-Object { $_ -ne '* hovud' -and $_ -ne 'hovud' } | ForEach-Object { git branch -d $_ }
```
Her er hovudgreina eksplisitt spesifiert som `hovud`. Det må endrast for kva enn depot du arbeidar i.

##### Utan å vite hovudgreina
```ps
$hovudgrein = (git remote show origin | ForEach-Object { $_.Trim() } | Where-Object { $_ -match "HEAD branch:" } | ForEach-Object { $_ -replace "HEAD branch:", '' })

git branch | ForEach-Object { $_.Trim() } | Where-Object { $_ -ne "* $hovudgrein" -and $_ -ne $hovudgrein } | ForEach-Object { git branch -d $_ }
```


### Gitub-aksjon (ubuntu-latest)
#### Sjekke om du har endra på filar i ei gitt mappe frå hovudgreina
```ps
git diff --name-only origin/${{ github.event.pull_request.base.ref }} HEAD | grep -qE .*src/${{ env.project }}/.*
```

`.*src/${{ env.project }}/.*` er regex for dei filane du vil sjekke. Den her vil spesifikt sjekke om ei fil sitt fulle namn inneheld `src/<INNHALD AV VARIABEL>/`. I depoet denne aksjonen ble skrevet for så var strukturen at kvart prosjekt lå i eiga mappe i `src/`. 
