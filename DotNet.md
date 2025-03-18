# ngrok

```
npm i ngrok -g
ngrok authtoken token
ngrok http https://localhost:44327
ngrok http --host-header=rewrite  https://localhost:3000
```


To make a summary, RESTful api can have arguments in several places:

In the request body - As part of a json body, or other MIME type
In the query string - e.g. /api/resource?p1=v1&p2=v2
As part of the URL-path - e.g. /api/resource/v1/v2
And you might see following attributes:

[FromQuery] (Gets values from the query string)
[FromUri] (This is not existing in dot net core, could ignore)
[FromRuote] (same as [Route(...)], Gets values from route data)
[FromForm] (Gets values from the posted form fields, content type of "application/x-www-url-formencoded ")
[FromBody] (Gets values from the request body, content type of "application/json")
[FromHeader] (Gets values from HTTP headers)
What I like to see:
HttpGet:
use path parameter or query parameter or both.

When simple use path. (e.g. get worker by id, [Route("api/worker/{id: int}"]) and
When complex use query. (e.g. api/worker?name=jack&gendar=1) and make request as class
When more complex try from body (e.g. api/worker , request body: {disable: true, createTime: "2021-02-01TZ00:00:00"}).
HttpPost/HttpPut:
use path + body (e.g. api/worker/2, request body:{ name: "jack", place: "Auckland"})

HttpDelete:
use path

About the search endpoint and next step, I like the GraphQL's design that use dynamic response fields which has a better performance. See Azure Search, give the response fields and query as parameter.

(e.g. GET [Organization URI]/api/data/v9.1/accounts?select=name&filter=Account_Emails/any(o:contains(o/subject,'sometext')))


# EF Core 8

### 1. Overriding SaveChanges or SaveChangesAsync

```Csharp
public override int SaveChanges()
{
    
    foreach (var entry in ChangeTracker.Entries())
    {
        if (entry.State == EntityState.Modified)
        {
            entry.Property("ModifiedTimestamp").CurrentValue = DateTime.UtcNow;
            entry.Property("ModifiedByUser").CurrentValue = GetCurrentUser();
        }

        return base.SaveChanges();
    }
}
```

- ✅ Automatic Auditing  
Ensures every change gets a ModifiedTimestamp and ModifiedByUser without manual updates.
- ✅ Better Maintainability  
Easy to extend (e.g., adding CreatedTimestamp).
- ✅ Handle Soft Deletes   
- ✅ Reduce Code Duplication and Less boilerplate code

### 2. No Track Queries and DbContexts
When no tracking is suitable for most query, better to set all queries for DbContext default to no tracking.

```Csharp
optionsBuilder
.UseSqlServer(myconnectionString)
.UseQueryTrackingBehavior(QueryTrackingBehavior.NoTracking)
```

### 3. Use EF Core async methods 
Using EF Core async methods is crucial for performance and responsiveness.

In a WinForms application, the UI runs on the main thread. If you run synchronous database operations, the UI thread gets blocked, making the application unresponsive (freezing).

Using EF Core async methods (FirstAsync(), ToListAsync()) allows database queries to run in the background without blocking the UI, keeping the app smooth and responsive.

✅ Using async EF Core methods (ToListAsync(), FirstAsync()) prevents UI freezing by offloading the database query to a background thread.

❌ Bad: Synchronous Query (Freezes UI)
csharp
Copy
Edit
private void LoadData()
{
    var users = _context.Users.ToList(); // Blocks UI thread
    dataGridView.DataSource = users; 
}
🚨 Issue: If the query takes time, the UI becomes unresponsive until it completes.

✅ Good: Async Query (Keeps UI Responsive)
csharp
Copy
Edit
private async void LoadDataAsync()
{
    var users = await _context.Users.ToListAsync(); // Runs on background thread
    dataGridView.DataSource = users; // UI remains responsive
}
🎯 Benefit: The UI stays responsive while the database query runs in the background.

2. Avoids "Not Responding" Errors
🔹 In a WinForms app, if the UI thread is blocked for too long, Windows may show "Not Responding" in the title bar.
🔹 This happens if a database query is slow and the UI thread is busy waiting.

✅ With async EF Core queries, the UI thread remains free, preventing "Not Responding" errors.

3. Improves Performance and Scalability
🔹 Synchronous queries make the app sluggish, especially when handling large datasets or slow queries.
🔹 Async queries allow other UI operations (like animations, progress bars, and user interactions) to continue smoothly.

Example: Using Async to Improve Performance with Progress Bar

csharp
Copy
Edit
private async void LoadDataWithProgressAsync()
{
    progressBar.Visible = true;
    
    var users = await _context.Users.ToListAsync(); // Runs on background thread
    
    dataGridView.DataSource = users;
    progressBar.Visible = false;
}
🎯 Benefit: The UI can show progress, improving user experience.

4. Prevents Deadlocks
🔹 Calling ToList() synchronously in an async event handler can cause deadlocks.
🔹 This happens when the UI thread waits for the database while the database waits for the UI thread, leading to a deadlock situation.

✅ Using await prevents deadlocks by allowing the database operation to complete without blocking the UI.

5. Best Practice for Modern C# Applications
🔹 Microsoft recommends using async methods in UI and web applications.
🔹 Future-proofing – EF Core and C# are moving towards async-first development.
🔹 Better Cloud & Database Performance – Async methods work well with remote databases like Azure SQL, where network latency exists.

When to Use EF Core Async in WinForms?
- ✅ Use ToListAsync(), FirstAsync(), etc., for all database queries.
- ✅ Always use async event handlers (async void) in UI code.
- ✅ Display progress indicators if queries take time.

Final Recommendation
💡 Always use EF Core async methods in C# WinForms applications to keep the UI responsive, avoid freezing, and improve performance. 🚀

### 4. 