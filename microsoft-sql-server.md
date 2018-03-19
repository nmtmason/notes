# Microsoft SQL Server

## Enabling TCP Connections

When installing SQL Server 2017 Developer Edition, connections over TCP/IP are disabled by default. Enable them as below:

1.  Open SQL Server Configuration Manager.
2.  Navigate to `SQL Server Network Configuration` > `Protocols`
3.  Enable the `TCP/IP` connection.

## Enable SQL Server Authentication Mode

By default, authentication is set to Windows Authentication only by default. To enable connections from database users enable the SQL Server Authentication Mode as below.

1.  Open the Microsoft SQL Server Management Studio.
2.  Create a new connection using your Windows credentials.
3.  Right-click the connection in the explorer window and select `Properties`.
4.  Select the `Security` page.
5.  Under `Server Authentication` ensure that the `SQL Server and Windows Authentication mode` is selected.
