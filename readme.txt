Prerequisite: .NET 7.0

To test the application:

1) Start a docker SQL-Server container with:

    docker run --cap-add SYS_PTRACE -e ACCEPT_EULA=1 -e MSSQL_SA_PASSWORD=SqlPassword! -p 1444:1433 --name azsql -d mcr.microsoft.com/azure-sql-edge

2) Create database in SQL Server named 'NewOrleans' then run following SQL scripts.

    SQLServer-Main.sql
    SQLServer-Persistence.sql
    SQLServer-Clustering.sql
    SQLServer-Reminders.sql

Reference: https://learn.microsoft.com/en-us/dotnet/orleans/host/configuration-guide/adonet-configuration

3) start first silo with:

    dotnet run 11111

4) start the API project (SQLServer-Reminders.sql) with:

    dotnet watch

5) Use swagger UI to increment & decrement numbers.

If using postman with key 'fred', try these:

- http://localhost:5000/inrcement/fred
- http://localhost:5000/decrement/fred

6) Look at the database tables to get a sense of stored data

7) start second clustered silo with:

    dotnet run 22222

    - In the silo terminal windows you will notice that both silos are recognizing one another.

    - In the OrleansMembershipTable you will notice that another row is added for the second silo.

    - Run more requests and you will see that they are routed to different silos.

NOTE:
ConnectionString = @"Data Source=localhost,1444;Database=NewOrleans;Persist Security Info=True;User ID=sa;Password=SqlPassword!;TrustServerCertificate=True;";

Reference: 
https://bogdan-dina03.medium.com/running-a-cluster-of-microsoft-orleans-virtual-actors-e755ace1750
