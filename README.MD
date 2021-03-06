# Start

## Database Instance

* Make sure you have installed LocalDB on your system.
* Make sure there is an instance called `ServiceQ` within LocalDB.
* [If not get `SqlLocalDB.MSI` now.](http://www.microsoft.com/en-us/download/details.aspx?id=29062 "Download it")
* (You may need to restart your computer.)
* [Add the instance using this guide.](https://www.mssqltips.com/sqlservertip/2694/getting-started-with-sql-server-2012-express-localdb/ "Read more")
  * Run the command: `SqlLocalDb create "ServiceQ" -s`
* Do not modify appsettings.json!

## Database Tables

* Make sure you have installed ASP.NET 5
* Make sure to install/upgrade the `dnvm` command

[Follow this giude](http://docs.asp.net/en/latest/getting-started/installing-on-windows.html "Right now") on details for both. You may need to restart after installing ASP.NET 5.

Afterwards, you can migrate the database.

* Using the command prompt go to the `src/ServiceQuality` directory
* Run the command: `dnx ef database update`

You'll see the following as it generates the database.

```
Applying migration '00000000000000_CreateIdentitySchema'.
Applying migration
Done.
```

## Run the App

* (Again) Make sure you have installed ASP.NET 5

Simply press the green play button on Visual Studio! If you do not see "IIS Express" as the option to run, go to the previous step and install ASP.NET 5.

After starting, the browser will open to the Service page.

You'll see a "Create" link near the top, so create a new service.

Start modifying the `ServiceController` and anything else!

## Use the App
After you get it running...

1. On the Index page, click "Create New".
2. Fill in the test name of your desire in the "Name" field (i.e. "test 1").
3. Fill in the URL of the web service you want the test to ping and calculate response time of.
4. If applicable, a dropdown menu of methods will appear. Select one.
5. If application, the corresponding fields of parameter(s) for the selected method will appear. Fill in the parameter(s).
6. Fill in number of requests you want the test to send (anything beyond 500 will be slow).
7. Select the test type you want to run: Capacity - requests will be sent sequantially and you will be able to monitor a smooth moving chart of the response time; Distribution - all requests will be sent at once, you will still be able to monitor the response time but at a different pace.
8. Click "Create" to create the test, you will be directed to the "Service Performance" page. NOTE: at this point the test is not running yet.
9. Click "Begin Service Test", the backend will start sending the requests to the designated server depending on the test type. As soon as you do this, the gauge and chart will start moving, reflecting the real-time response time for the requests.
* The "Stop" button stops this real-time monitoring; the "Start" button starts the real-time monitoring.
10. Once the requests stop sending (either finished or error-ed out), the gauge and chart should stop moving. At this point...
* If you've selected the "Capacity" test, click the "Statistics" button to populate the "Avg. Performance", "Capacity", and "Reliability". The "Distribution" chart will not populate.
* If you've selected the "Distribution" test, there will be a "Distribution Base" field. Fill in a number for the base, this is for displaying the distribution in a power of the base request counts (i.e. if you fill in 5, it will show average response time of 5 requests, 25 requests, 125 requests... until the largest power of 5 less than the total requests sent).

To compare between test results...

1. Click "Compare Tests" on the top
2. Use the 2 dropdown menu to selet existing test results (you might have to wait for a bit for them to populate)
3. Fill in a number for the "Distribution Base", this will be used to calculate and populate the distribution data points
4. Click "Compare" and see the various tests results list side by side
