# Nyttige kommandoar for terminalar
Du kan lese [ordliste ved botn av dokumentet](#ordliste).


## Git
### PowerShell
#### Slette alle avgreiningar frå hovudgreina som er samenslått med hovudgreina.
```ps
git branch | ForEach-Object { $_.Trim() } | Where-Object { $_ -ne '* test'} | ForEach-Object { git branch -d $_ }
```
Her er hovudgreina eksplisitt spesifiert som `test`. Det må endrast for kva enn depot du arbeidar i.

### Gitub-aksjon (ubuntu-latest)
#### Sjekke om du har endra på filar i ei gitt mappe frå hovudgreina
```ps
git diff --name-only origin/${{ github.event.pull_request.base.ref }} HEAD | grep -qE .*src/${{ env.project }}/.*
```

`.*src/${{ env.project }}/.*` er regex for dei filane du vil sjekke. Den her vil spesifikt sjekke om ei fil sitt fulle namn inneheld `src/<INNHALD AV VARIABEL>/`. I depoet denne aksjonen ble skrevet for så var strukturen at kvart prosjekt lå i eiga mappe i `src/`. 



## Ordliste
Norsk           | Engelsk 
:--             | :-- 
Depot           | Repository
Grein           | Default branch
Avgreining      | Branch which is not default branch
Github-aksjon   | GitHub Action
