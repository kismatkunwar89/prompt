generate for During a forensic investigation of a Windows NTFS system, the Master File Table (C:\$MFT) was parsed. Investigators extracted several file records linked to the user profile C:\Users\Alice\.

Multiple .lnk shortcut files and their associated targets were identified across distinct MFT records. Most shortcut relationships were timestamp-consistent. However, one .lnk file referencing password.docx was created **before** the target file existed, suggesting a possible anti-forensics artifact.

Below are the artifacts from the parsed MFT:

Artifact 1: password.docx  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116327  
- File Name: password.docx  
- Path: C:\Users\Alice\Documents\password.docx  
- Extension: .docx  
- Creation Time (NTFS 0x10): 2025-03-04T10:15:00Z  

Artifact 2: password.lnk  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116328  
- File Name: password.lnk  
- Path: C:\Users\Alice\AppData\Roaming\Microsoft\Windows\Recent\password.lnk  
- Extension: .lnk  
- Creation Time (NTFS 0x10): 2025-03-04T01:10:00Z  
- Local Base Path (parsed from LNK metadata): C:\Users\Alice\Documents\password.docx  

Artifact 3: budget.xlsx  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116329  
- File Name: budget.xlsx  
- Path: C:\Users\Alice\Documents\budget.xlsx  
- Extension: .xlsx  
- Creation Time (NTFS 0x10): 2025-03-01T13:00:00Z  

Artifact 4: budget.lnk  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116330  
- File Name: budget.lnk  
- Path: C:\Users\Alice\AppData\Roaming\Microsoft\Windows\Recent\budget.lnk  
- Extension: .lnk  
- Creation Time (NTFS 0x10): 2025-03-01T13:15:00Z  
- Local Base Path (parsed from LNK metadata): C:\Users\Alice\Documents\budget.xlsx  

Artifact 5: confidential.txt  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116331  
- File Name: confidential.txt  
- Path: C:\Users\Alice\Desktop\confidential.txt  
- Extension: .txt  
- Creation Time (NTFS 0x10): 2025-03-02T09:00:00Z  

Artifact 6: confidential.lnk  
- Source: MFT record from C:\$MFT  
- MFT Record Number: 116332  
- File Name: confidential.lnk  
- Path: C:\Users\Alice\AppData\Roaming\Microsoft\Windows\Recent\confidential.lnk  
- Extension: .lnk  
- Creation Time (NTFS 0x10): 2025-03-02T09:10:00Z  
- Local Base Path (parsed from LNK metadata): C:\Users\Alice\Desktop\confidential.txt

```json {
  "@context": {
    "kb": "http://example.org/kb/",
    "uco-core": "https://ontology.unifiedcyberontology.org/uco/core/",
    "uco-observable": "https://ontology.unifiedcyberontology.org/uco/observable/",
    "uco-types": "https://ontology.unifiedcyberontology.org/uco/types/",
    "xsd": "http://www.w3.org/2001/XMLSchema#"
  },
  "@graph": [
    {
      "@id": "kb:file-123e4567-e89b-12d3-a456-426614174000",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-123e4567-e89b-12d3-a456-426614174001",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "password.docx",
          "uco-observable:filePath": "C:\\Users\\Alice\\Documents\\password.docx",
          "uco-observable:extension": "docx",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-04T10:15:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:file-123e4567-e89b-12d3-a456-426614174002",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-123e4567-e89b-12d3-a456-426614174003",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "password.lnk",
          "uco-observable:filePath": "C:\\Users\\Alice\\AppData\\Roaming\\Microsoft\\Windows\\Recent\\password.lnk",
          "uco-observable:extension": "lnk",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-04T01:10:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:file-123e4567-e89b-12d3-a456-426614174004",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-123e4567-e89b-12d3-a456-426614174005",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "budget.xlsx",
          "uco-observable:filePath": "C:\\Users\\Alice\\Documents\\budget.xlsx",
          "uco-observable:extension": "xlsx",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-01T13:00:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:file-123e4567-e89b-12d3-a456-426614174006",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-123e4567-e89b-12d3-a456-426614174007",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "budget.lnk",
          "uco-observable:filePath": "C:\\Users\\Alice\\AppData\\Roaming\\Microsoft\\Windows\\Recent\\budget.lnk",
          "uco-observable:extension": "lnk",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-01T13:15:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:file-123e4567-e89b-12d3-a456-426614174008",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-123e4567-e89b-12d3-a456-426614174009",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "confidential.txt",
          "uco-observable:filePath": "C:\\Users\\Alice\\Desktop\\confidential.txt",
          "uco-observable:extension": "txt",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-02T09:00:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:file-123e4567-e89b-12d3-a456-426614174010",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-123e4567-e89b-12d3-a456-426614174011",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "confidential.lnk",
          "uco-observable:filePath": "C:\\Users\\Alice\\AppData\\Roaming\\Microsoft\\Windows\\Recent\\confidential.lnk",
          "uco-observable:extension": "lnk",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-02T09:10:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:relationship-123e4567-e89b-12d3-a456-426614174012",
      "@type": "uco-observable:ObservableRelationship",
      "uco-core:source": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174002" },
      "uco-core:target": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174000" },
      "uco-core:kindOfRelationship": "Referenced_Within",
      "uco-core:isDirectional": true
    },
    {
      "@id": "kb:relationship-123e4567-e89b-12d3-a456-426614174013",
      "@type": "uco-observable:ObservableRelationship",
      "uco-core:source": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174006" },
      "uco-core:target": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174004" },
      "uco-core:kindOfRelationship": "Referenced_Within",
      "uco-core:isDirectional": true
    },
    {
      "@id": "kb:relationship-123e4567-e89b-12d3-a456-426614174014",
      "@type": "uco-observable:ObservableRelationship",
      "uco-core:source": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174010" },
      "uco-core:target": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174008" },
      "uco-core:kindOfRelationship": "Referenced_Within",
      "uco-core:isDirectional": true
    }
  ]
}
Here is the JSON-LD output based on your scenario. Would you like to make any changes? Please validate the output using case_validate from the case_utils package to ensure compliance with the CASE/UCO ontology.

Here is a generic SPARQL query to detect timestamp inconsistencies where a .lnk file references a target file but was created before the target file existed. This query flags potential anti-forensics artifacts:

sparql
Copy
PREFIX uco-core: <https://ontology.unifiedcyberontology.org/uco/core/>
PREFIX uco-observable: <https://ontology.unifiedcyberontology.org/uco/observable/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?lnkFile ?lnkCreationTime ?targetFile ?targetCreationTime
WHERE {
  # Identify the .lnk file and its creation time
  ?lnkFile a uco-observable:File ;
           uco-core:hasFacet ?lnkFacet .
  ?lnkFacet a uco-observable:FileFacet ;
            uco-observable:extension "lnk" ;
            uco-observable:observableCreatedTime ?lnkCreationTime .

  # Identify the relationship between the .lnk file and its target file
  ?relationship a uco-observable:ObservableRelationship ;
                uco-core:source ?lnkFile ;
                uco-core:target ?targetFile ;
                uco-core:kindOfRelationship "Referenced_Within" .

  # Identify the target file and its creation time
  ?targetFile a uco-observable:File ;
              uco-core:hasFacet ?targetFacet .
  ?targetFacet a uco-observable:FileFacet ;
               uco-observable:observableCreatedTime ?targetCreationTime .

  # Filter for cases where the .lnk file was created before the target file
  FILTER (?lnkCreationTime < ?targetCreationTime)
}
Explanation of the Query:
Identify .lnk Files:

The query selects files with the .lnk extension and retrieves their creation timestamps (?lnkCreationTime).

Identify Relationships:

It looks for ObservableRelationship instances where the .lnk file (?lnkFile) references a target file (?targetFile) with the relationship type "Referenced_Within".

Identify Target Files:

The query retrieves the creation timestamps (?targetCreationTime) of the target files referenced by the .lnk files.

Filter for Inconsistencies:

The FILTER clause checks if the .lnk file's creation time (?lnkCreationTime) is earlier than the target file's creation time (?targetCreationTime), flagging potential inconsistencies.

Output:

The query returns the .lnk file, its creation time, the target file, and the target file's creation time for further investigation.

Example Output:
If the .lnk file password.lnk was created at 2025-03-04T01:10:00Z but references password.docx created at 2025-03-04T10:15:00Z, the query would return:

?lnkFile	?lnkCreationTime	?targetFile	?targetCreationTime
kb:file-123e4567-e89b-12d3...	2025-03-04T01:10:00Z	kb:file-123e4567-e89b-12d3...	2025-03-04T10:15:00Z
This output highlights the inconsistency, suggesting a potential anti-forensics artifact.

Would you like to refine this query further or apply it to a specific dataset?

have file name instead
Here is the updated SPARQL query that includes the file names of both the .lnk file and the target file, making it easier to identify the specific files involved in the timestamp inconsistency:

sparql
Copy
PREFIX uco-core: <https://ontology.unifiedcyberontology.org/uco/core/>
PREFIX uco-observable: <https://ontology.unifiedcyberontology.org/uco/observable/>
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>

SELECT ?lnkFileName ?lnkCreationTime ?targetFileName ?targetCreationTime
WHERE {
  # Identify the .lnk file, its name, and its creation time
  ?lnkFile a uco-observable:File ;
           uco-core:hasFacet ?lnkFacet .
  ?lnkFacet a uco-observable:FileFacet ;
            uco-observable:fileName ?lnkFileName ;
            uco-observable:extension "lnk" ;
            uco-observable:observableCreatedTime ?lnkCreationTime .

  # Identify the relationship between the .lnk file and its target file
  ?relationship a uco-observable:ObservableRelationship ;
                uco-core:source ?lnkFile ;
                uco-core:target ?targetFile ;
                uco-core:kindOfRelationship "Referenced_Within" .

  # Identify the target file, its name, and its creation time
  ?targetFile a uco-observable:File ;
              uco-core:hasFacet ?targetFacet .
  ?targetFacet a uco-observable:FileFacet ;
               uco-observable:fileName ?targetFileName ;
               uco-observable:observableCreatedTime ?targetCreationTime .

  # Filter for cases where the .lnk file was created before the target file
  FILTER (?lnkCreationTime < ?targetCreationTime)
}
Explanation of Changes:
Added File Names:

The query now retrieves the uco-observable:fileName for both the .lnk file (?lnkFileName) and the target file (?targetFileName).

Output:

The query returns the .lnk file name, its creation time, the target file name, and the target file's creation time.

Example Output:
If the .lnk file password.lnk was created at 2025-03-04T01:10:00Z but references password.docx created at 2025-03-04T10:15:00Z, the query would return:

?lnkFileName	?lnkCreationTime	?targetFileName	?targetCreationTime
password.lnk	2025-03-04T01:10:00Z	password.docx	2025-03-04T10:15:00Z
This output provides a clear and human-readable summary of the inconsistency, making it easier to identify potential anti-forensics artifacts.

Would you like to refine this query further or apply it to a specific dataset?

