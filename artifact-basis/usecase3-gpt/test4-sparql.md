Here's a generic SPARQL query designed to detect inconsistencies where a successful Windows logon event exists for a user (e.g., john.doe), but no matching profile folder exists under C:\Users\.

This query assumes:

Logon events are modeled using a custom facet (acme:WindowsLogonEventFacet) with acme:accountName.
User profile directories are represented as uco-observable:Directory with paths under C:\Users\.
✅ SPARQL Query for Detecting Missing User Profile Directory
sparql
Copy
Edit
PREFIX uco-core: <https://ontology.unifiedcyberontology.org/uco/core/>
PREFIX uco-observable: <https://ontology.unifiedcyberontology.org/uco/observable/>
PREFIX acme: <http://example.org/custom-ns/acme#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT DISTINCT ?accountName
WHERE {
  # Step 1: Find usernames from successful logon events (Event ID 4624)
  ?logonEntity a uco-observable:AutonomousSystem ;
               uco-core:hasFacet ?logonFacet .
  ?logonFacet a acme:WindowsLogonEventFacet ;
              acme:eventID "4624" ;
              acme:accountName ?accountName .

  # Step 2: Ensure there's no directory for that account under C:\Users\
  FILTER NOT EXISTS {
    ?dir a uco-observable:Directory ;
         uco-core:hasFacet ?dirFacet .
    ?dirFacet a uco-observable:FileFacet ;
              uco-observable:filePath ?path ;
              uco-observable:isDirectory true .
    
    # Normalize and check path match
    FILTER regex(?path, CONCAT("^C:\\\\Users\\\\", ?accountName, "$"), "i")
  }
}
💡 Result
This query returns usernames that:

Had a successful logon (eventID = 4624).
But don’t have a matching C:\Users\<username> directory.
Would you like a version that also checks for partial folder matches like C:\Users\john.doe.DOMAIN?





You said:
now  generate an generic sparql to detect inconsistency john doe user was still present in the system's registry account list.  but no corresponding user profile folder existed
ChatGPT said:
Here’s a generic SPARQL query to detect the inconsistency where a username (e.g., john.doe) is present in the Windows Registry under SAM\\Domains\\Account\\Users\\Names, but no corresponding C:\Users\john.doe profile folder exists.

✅ SPARQL Query to Detect Users in Registry but Missing Profile Folder
sparql
Copy
Edit
PREFIX uco-core: <https://ontology.unifiedcyberontology.org/uco/core/>
PREFIX uco-observable: <https://ontology.unifiedcyberontology.org/uco/observable/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT DISTINCT ?username
WHERE {
  # Step 1: Extract usernames from registry keys like HKEY_LOCAL_MACHINE\SAM\...\Names\<username>
  ?regKey a uco-observable:WindowsRegistryKey ;
          uco-core:hasFacet ?regFacet .
  ?regFacet a uco-observable:WindowsRegistryKeyFacet ;
            uco-observable:key ?regPath .

  # Extract username from the registry path
  FILTER regex(?regPath, "^HKEY_LOCAL_MACHINE\\\\SAM\\\\Domains\\\\Account\\\\Users\\\\Names\\\\([^\\\\]+)$", "i")

  # Use a regex group to capture the username portion
  BIND(REPLACE(?regPath, "^.*\\\\Names\\\\", "") AS ?username)

  # Step 2: Ensure no corresponding C:\Users\<username> directory exists
  FILTER NOT EXISTS {
    ?dir a uco-observable:Directory ;
         uco-core:hasFacet ?dirFacet .
    ?dirFacet a uco-observable:FileFacet ;
              uco-observable:filePath ?dirPath ;
              uco-observable:isDirectory true .
    
    FILTER regex(?dirPath, CONCAT("^C:\\\\Users\\\\", ?username, "$"), "i")
  }
}
🧠 What This Detects
Finds users listed in the registry account list (under HKEY_LOCAL_MACHINE\SAM\...).
Checks if their profile directory is missing under C:\Users\.
Flags those usernames as inconsistent.
Would you like to combine this with the previous query to detect users who had either a logon event or were present in the registry, but had no corresponding profile directory?





You said:
yes
ChatGPT said:
Here’s a combined SPARQL query that detects usernames who:

Had a successful logon event (eventID = 4624),
OR are present in the Windows Registry account list,
BUT have no corresponding C:\Users\<username> directory.
✅ Combined SPARQL Query
sparql
Copy
Edit
PREFIX uco-core: <https://ontology.unifiedcyberontology.org/uco/core/>
PREFIX uco-observable: <https://ontology.unifiedcyberontology.org/uco/observable/>
PREFIX acme: <http://example.org/custom-ns/acme#>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT DISTINCT ?username
WHERE {
  {
    # From logon events (Event ID 4624)
    ?logonEntity a uco-observable:AutonomousSystem ;
                 uco-core:hasFacet ?logonFacet .
    ?logonFacet a acme:WindowsLogonEventFacet ;
                acme:eventID "4624" ;
                acme:accountName ?username .
  }
  UNION
  {
    # From registry key path ending in \Names\<username>
    ?regKey a uco-observable:WindowsRegistryKey ;
            uco-core:hasFacet ?regFacet .
    ?regFacet a uco-observable:WindowsRegistryKeyFacet ;
              uco-observable:key ?regPath .

    FILTER regex(?regPath, "^HKEY_LOCAL_MACHINE\\\\SAM\\\\Domains\\\\Account\\\\Users\\\\Names\\\\([^\\\\]+)$", "i")
    BIND(REPLACE(?regPath, "^.*\\\\Names\\\\", "") AS ?username)
  }

  # Filter out usernames that DO have a corresponding C:\Users\<username> directory
  FILTER NOT EXISTS {
    ?dir a uco-observable:Directory ;
         uco-core:hasFacet ?dirFacet .
    ?dirFacet a uco-observable:FileFacet ;
              uco-observable:filePath ?dirPath ;
              uco-observable:isDirectory true .

    FILTER regex(?dirPath, CONCAT("^C:\\\\Users\\\\", ?username, "$"), "i")
  }
}
🔍 What This Catches
Any ?username that is:
Logged on (event 4624), or
Present in the registry key path
But does not have a C:\Users\?username directory.
Let me know if you want to expand this to handle:

Case-insensitive folder matches,
Domain-qualified usernames (e.g., john.doe.DOMAIN),
Timestamps for when logons occurred vs. expected profile creation.