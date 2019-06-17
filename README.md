# SignalR-Core-SqlTableDependencyMasterSample
 SignalR-Core-SqlTableDependency Core 2.2 sample (Copy from elvanydev.com posted on Aug 2017)

Ref: http://elvanydev.com/SignalR-Core-SqlDependency-part2/
source: https://github.com/vany0114/SignalR-Core-SqlTableDependency


This source has been modifier for Core 2.2 due to origional source is Core 1

Refer to Origional ReadMe From elvanydev.com.md for full instructions

SQL server Setup

-Enable the SQL Service Broker on the desired database
	ALTER DATABASE MyDatabase SET ENABLE_BROKER

-Check if Service Broker has been enabled
	SELECT is_broker_enabled FROM sys.databases WHERE name = 'Database_name';

-Disable the SQL Service Broker on the desired database
	ALTER DATABASE MyDatabase SET DISABLE_BROKER


For real-time update from database, this project use SqlTableDependency by Christian Del Bianco
Key featuer are in the InventoryDatabaseSubscription.cs file wil setup from the Startup.ConfigureServices()
by using dependency injection

The  InventoryDatabaseSubscription.Configure() method dictated what is monitoring. 
e.g.  _tableDependency = new SqlTableDependency<Product>(connectionString, null, null, null, null, null, DmlTriggerType.Delete);
will monitor all tables but fire only when a recrod deletion is happened 
then the changes will alert the SignalR Core to update application.


For performance comparision

https://stackoverflow.com/questions/39709395/sqldependency-performance
