Prerequisite: .NET 7.0

To test the appliation:

1) Start a docker SQL-Server container with:

    docker run --cap-add SYS_PTRACE -e ACCEPT_EULA=1 -e MSSQL_SA_PASSWORD=SqlPassword! -p 1444:1433 --name azsql -d mcr.microsoft.com/azure-sql-edge

2) Create database in SQL Server named 'NewOrleans' then run following SQL scripts.

    SQLServer-Main.sql
    SQLServer-Persistence.sql
    SQLServer-Clustering.sql
    SQLServer-Reminders.sql

3) start the silo with:

    dotnet run 11111

4) start the API project (SQLServer-Reminders.sql) with:

    dotnet watch

5) Use swagger UI to increment & decrement numbers.

If using postman with key 'fred', try these:

- http://localhost:5000/inrcement/fred
- http://localhost:5000/decrement/fred

6) Look at the database tables to get a sense of stored data

NOTE:
ConnectionString = @"Data Source=localhost,1444;Database=NewOrleans;Persist Security Info=True;User ID=sa;Password=SqlPassword!;TrustServerCertificate=True;";