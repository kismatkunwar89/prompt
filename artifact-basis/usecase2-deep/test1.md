Please provide the details of your cyber investigation scenario or artifact.

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
```json 
Copy
{
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
      "@id": "kb:relationship-123e4567-e89b-12d3-a456-426614174004",
      "@type": "uco-observable:ObservableRelationship",
      "uco-core:source": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174002" },
      "uco-core:target": { "@id": "kb:file-123e4567-e89b-12d3-a456-426614174000" },
      "uco-core:kindOfRelationship": "Referenced_Within",
      "uco-core:isDirectional": true
    }
  ]
}
Here is the JSON-LD output based on your scenario. Would you like to make any changes? Please validate the output using case_validate from the case_utils package to ensure compliance with the CASE/UCO ontology.
