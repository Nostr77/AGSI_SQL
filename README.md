# AGSI_SQL
Azure Database SQL + PowerBI 

Data description and preparatory python script you can find here.  
[1. PowerBI & Python. Automatic Analytical Dashboard based on PowerBI and Python. From API to Dashboard, combining archive data with recent one](https://github.com/Nostr77/AGSI)

## SQL part of dashboard
![Schema](https://github.com/Nostr77/AGSI_SQL/raw/main/Capture4.JPG)

## Power Query M 1. Finding last date in the Archive and make a API Online Direct Query update in PowerBI
![Schema](https://github.com/Nostr77/AGSI_SQL/raw/main/Capture9.JPG)

```
let
    
    SourceD = Sql.Database("nicucmb.database.windows.net,1433", "agsi"),
    dbo_o_last_day_archive = SourceD{[Schema="dbo",Item="o_last_day_archive"]}[Data],
    #"Changed TypeD" = Table.TransformColumnTypes(dbo_o_last_day_archive,{{"last_day_archive", type text}}),
    #"Changed Type1D" = Table.SelectRows(#"Changed TypeD", each not Text.Contains("last_day_archive", "B")),
    gasDayStart = #"Changed Type1D"[last_day_archive],
    #"Sorted ItemsD" = List.First(gasDayStart),
    
    Source1 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=AT&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table1" = Table.FromRecords({Source1}),
    
    Source2 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=BE&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table2" = Table.FromRecords({Source2}),
    
    Source3 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=BG&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table3" = Table.FromRecords({Source3}),
    
    Source4 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=CZ&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table4" = Table.FromRecords({Source4}),
    
    Source5 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=DE&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table5" = Table.FromRecords({Source5}),
    
    Source6 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=DK&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table6" = Table.FromRecords({Source6}),
    
    Source7 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=ES&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table7" = Table.FromRecords({Source7}),
    
    Source8 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=FR&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table8" = Table.FromRecords({Source8}),
    
    Source9 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=HR&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table9" = Table.FromRecords({Source9}),
    
    Source10 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=HU&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table10" = Table.FromRecords({Source10}),
    
    Source11 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=IT&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table11" = Table.FromRecords({Source11}),
    
    Source12 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=LV&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table12" = Table.FromRecords({Source12}),
    
    Source13 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=NL&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table13" = Table.FromRecords({Source13}),
    
    Source14 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=PL&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table14" = Table.FromRecords({Source14}),
    
    Source15 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=PT&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table15" = Table.FromRecords({Source15}),
    
    Source16 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=RO&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table16" = Table.FromRecords({Source16}),
    
    Source17 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=SE&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table17" = Table.FromRecords({Source17}),
    
    Source18 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=SK&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table18" = Table.FromRecords({Source18}),
    
    Source19 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=UA&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table19" = Table.FromRecords({Source19}),
    
    Source20 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=IE&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table20" = Table.FromRecords({Source20}),
    
    Source21 = Json.Document(Web.Contents("https://agsi.gie.eu/api?country=GB*&from="&#"Sorted ItemsD"&"&to="&Date.ToText(Date.AddDays(Date.From(DateTime.LocalNow()),0),"yyyy-MM-dd")&"&page=1&size=150")),
    #"Converted to Table21" = Table.FromRecords({Source21}),
    
    
    #"Converted to Table" = Table.Combine({ #"Converted to Table1", #"Converted to Table2", #"Converted to Table3", #"Converted to Table4", #"Converted to Table5", #"Converted to Table6", #"Converted to Table7", #"Converted to Table8", #"Converted to Table9", #"Converted to Table10", #"Converted to Table11", #"Converted to Table12", #"Converted to Table13", #"Converted to Table14", #"Converted to Table15", #"Converted to Table16", #"Converted to Table17", #"Converted to Table18", #"Converted to Table19",  #"Converted to Table21"}),
    
    #"Expanded data" = Table.ExpandListColumn(#"Converted to Table", "data"),
    
    #"Expanded data1" = Table.ExpandRecordColumn(#"Expanded data", "data", {"code", "url", "gasDayStart", "gasInStorage", "consumption", "consumptionFull", "injection", "withdrawal", "netWithdrawal", "workingGasVolume", "injectionCapacity", "withdrawalCapacity", "status", "trend", "full"}, {"data.code", "data.url", "data.gasDayStart", "data.gasInStorage", "data.consumption", "data.consumptionFull", "data.injection", "data.withdrawal", "data.netWithdrawal", "data.workingGasVolume", "data.injectionCapacity", "data.withdrawalCapacity", "data.status", "data.trend", "data.full"}),
    #"Changed Type" = Table.TransformColumnTypes(#"Expanded data1",{{"data.code", type text}, {"data.url", type text}, {"data.gasDayStart", type date}, {"data.gasInStorage", type number}, {"data.consumption", type number}, {"data.consumptionFull", type number}, {"data.injection", type number}, {"data.withdrawal", type number}, {"data.netWithdrawal", type number}, {"data.workingGasVolume", type number}, {"data.injectionCapacity", type number}, {"data.withdrawalCapacity", type number}, {"data.status", type text}, {"data.trend", type number}, {"data.full", type number}}),
    #"Added Custom" = Table.AddColumn(#"Changed Type", "data.code1", each Text.Range([data.code],0,2)),
    #"Added Custom10" = Table.AddColumn(#"Added Custom", "data.url1", each Text.Range([data.url],0,2)),
    #"Removed Columns" = Table.RemoveColumns(#"Added Custom10",{"last_page", "total", "dataset", "gas_day"}),
    #"Renamed Columns" = Table.RenameColumns(#"Removed Columns",{{"data.code1", "code"}, {"data.url1", "url"}, {"data.gasDayStart", "gasDayStart"}, {"data.gasInStorage", "gasInStorage"}, {"data.consumption", "consumption"}, {"data.consumptionFull", "consumptionFull"}, {"data.injection", "injection"}, {"data.withdrawal", "withdrawal"}, {"data.netWithdrawal", "netWithdrawal"}, {"data.workingGasVolume", "workingGasVolume"}, {"data.injectionCapacity", "injectionCapacity"}, {"data.withdrawalCapacity", "withdrawalCapacity"}, {"data.status", "status"}, {"data.trend", "trend"}, {"data.full", "full_"}}),
    table0=#"Renamed Columns",



changetype = Table.TransformColumnTypes(table0,{{"gasDayStart", type text},{"gasInStorage", type text},{"consumption", type text},{"consumptionFull", type text},{"injection", type text},{"withdrawal", type text},{"netWithdrawal", type text},{"workingGasVolume", type text},{"injectionCapacity", type text},{"withdrawalCapacity", type text},{"trend", type text},{"full_", type text} }, "en-CA"),

#"Grouped Rows" = Table.CombineColumns(changetype, {"code", "url", "gasDayStart", "gasInStorage", "consumption", "consumptionFull", "injection", "withdrawal", "netWithdrawal", "workingGasVolume", "injectionCapacity", "withdrawalCapacity", "status", "trend", "full_"} ,
    Combiner.CombineTextByDelimiter("','", QuoteStyle.None),
    "FullName" as text
),
    #"Removed Columns1" = Table.RemoveColumns(#"Grouped Rows",{"data.code"}),
    #"Removed Columns2" = Table.RemoveColumns(#"Removed Columns1",{"data.url"}),
    #"Added Custom1" = Table.AddColumn(#"Removed Columns2", "Custom", each 1),

#"Grouped Rows2" = Table.Group(#"Added Custom1"  ,{"Custom"}, {{"FullNamePlus", each Text.Combine([FullName], "' ), ( '"), type text}}),

 #"Grouped Rows3" = Table.SelectRows(#"Grouped Rows2", each not Text.Contains("FullNamePlus", "B")),
 Query4 = "delete from agsi_sandbox;  INSERT INTO agsi_sandbox (code,url,gasDayStart,gasInStorage,consumption,consumptionFull,injection,withdrawal,netWithdrawal,workingGasVolume,injectionCapacity,withdrawalCapacity,status,trend,full_) values ('"&List.First(#"Grouped Rows3"[FullNamePlus])&"')",

SourceSQL = Sql.Database("nicucmb.database.windows.net, 1433", "agsi", [Query=Query4])

in
  SourceSQL
```


## Dashboard visuals (consists of (a) visual screenshot (b) SQL script (c) Result table

### 1 o_table.sql
![Schema](https://github.com/Nostr77/AGSI_SQL/raw/main/Capture5.JPG)

```
alter view o_table as
select 
	Country, Gas_in_Storage_TWh, Full_by_Countries, rank() over(order by dummy desc) as ranking 
from
	(select 
		grup as Country, 
		round(sum(gasinstorage),1) as Gas_in_Storage_TWh, 
		sum(gasinstorage*full_)/(sum(gasinstorage)*100) as Full_by_Countries, 
		EU, 
		(case  grup
		when 'Other' then 1000000
		else 1000000+sum(gasinstorage)
		end) as dummy
	from 
		(select *
		from agsi  
		union
		select *
		from agsi_sandbox) as a
		left join names as n
		on a.code=n.code
	where gasdaystart=(select max(gasdaystart) from 
							(select gasdaystart 
								from agsi  
								union
								select gasdaystart
								from agsi_sandbox) as a) and EU='EU'
	group by grup, gasdaystart,EU

	UNION

	select 
		'*** Total (EU)' as Country, 
		round(sum(gasinstorage),1) as Gas_in_Storage_TWh, 
		sum(gasinstorage*full_)/(sum(gasinstorage)*100) as Full_by_Countries, 
		EU,
		1000000-1 as dummy
	from 
			(select *
			from agsi  
			union
			select *
			from agsi_sandbox) as a
		left join names as n
		on a.code=n.code
	where gasdaystart=(select max(gasdaystart) from (select gasdaystart 
								from agsi  
								union
								select gasdaystart
								from agsi_sandbox) as a) and EU='EU'
	group by gasdaystart,EU  


	UNION

	select name as Country, 
		round(sum(gasinstorage),1) as Gas_in_Storage_TWh, 
		sum(gasinstorage*full_)/(sum(gasinstorage)*100) as Full_by_Countries, 
		EU, 
		1000+sum(gasinstorage) as dummy
	from 
				(select *
			from agsi  
			union
			select *
			from agsi_sandbox) as a
	left join names as n
		on a.code=n.code
	where gasdaystart=(select max(gasdaystart) from [dbo].[AGSI]) and EU='Non-EU'
	group by name, gasdaystart,EU

	UNION

	select 
		'*** Total (EU+NonEU)' as Country, 
		round(sum(gasinstorage),1) as Gas_in_Storage_TWh, 
		sum(gasinstorage*full_)/(sum(gasinstorage)*100) as Full_by_Countries, 
		'EU+NonEU' as EU,
		100-1 as dummy
	from 
				(select *
			from agsi  
			union
			select *
			from agsi_sandbox) as a
		left join names as n
		on a.code=n.code
	where gasdaystart=(select max(gasdaystart) from (select gasdaystart 
								from agsi  
								union
								select gasdaystart
								from agsi_sandbox) as a)
	group by gasdaystart
	) as a2

```

|Country	|Gas_in_Storage_TWh	|Full_by_Countries	|Ranking
|---	|---	|---	|---
|Germany	|241.2	|0.98	|1
|Italy	|177.3	|0.9163	|2
|France	|129.5	|0.9689	|3
|Netherlands	|123	|0.8855	|4
|Austria	|89.7	|0.9385	|5
|Poland	|35.4	|0.9734	|6
|Other	|234.1	|0.890446721981314	|7
|*** Total (EU)	|1030.2	|0.932169104411994	|8
|Ukraine	|99.1	|0.305	|9
|United Kingdom	|10.5	|1	|10
|*** Total (EU+NonEU)	|1137.8	|0.878612189282578	|11



### 2
![Schema](https://github.com/Nostr77/AGSI_SQL/raw/main/Capture6.JPG)
```
```

### 3
![Schema](https://github.com/Nostr77/AGSI_SQL/raw/main/Capture7.JPG)

```
```

### 4
![Schema](https://github.com/Nostr77/AGSI_SQL/raw/main/Capture8.JPG)

```
```



