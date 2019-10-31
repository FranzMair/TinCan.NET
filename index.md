---
layout: index
---

### Supported API Versions

**1.0.0** (1.0.1)

### Getting Started

Install 'TinCan' via NuGet or download dll from GitHub releases.

### Basic Usage

The following sample shows the most basic usage of TinCan.NET. There are *a lot* of other options, methods, and model elements, check the API documentation for more.

```csharp
using System;
using TinCan;
using TinCan.LRSResponses;

var lrs = new RemoteLRS(
    "https://cloud.scorm.com/tc/public/",
    "<username>",
    "<password>"
);

var actor = new Agent();
actor.mbox = "mailto:info@tincanapi.com";

var verb = new Verb();
verb.id = new Uri ("http://adlnet.gov/expapi/verbs/experienced");
verb.display = new LanguageMap();
verb.display.Add("en-US", "experienced");

var activity = new Activity();
activity.id = "http://rusticisoftware.github.io/TinCan.NET";

var statement = new Statement();
statement.actor = actor;
statement.verb = verb;
statement.target = activity;

StatementLRSResponse lrsResponse = lrs.SaveStatement(statement);
if (lrsResponse.success)
{
    // Updated 'statement' here, now with id
    Console.WriteLine("Save statement: " + lrsResponse.content.id);
}
else
{
    // Do something with failure
}
```

### Query to Get 10 Statements Since a Specific Time

```csharp
using System;
using TinCan;
using TinCan.LRSResponses;

var lrs = new RemoteLRS(
    "https://cloud.scorm.com/tc/public/",
    "<username>",
    "<password>"
);

var query = new StatementsQuery();
query.since = DateTime.ParseExact("2013-08-29 07:42:10Z", "u", System.Globalization.CultureInfo.InvariantCulture);
query.limit = 10;

StatementsResultLRSResponse lrsResponse = lrs.QueryStatements(query);
if (lrsResponse.success)
{
    // List of statements available
    Console.WriteLine("Count of statements: " + lrsResponse.content.statements.Count);
}
else
{
    // Do something with failure
}
```
