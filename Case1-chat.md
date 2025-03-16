Case scenario

During a digital forensics investigation of an NTFS file system, two files of interest were identified. File 1 details: - Filename: password.docx - Extension: .docx - Creation timestamp (recorded in the NTFS MFT record, attribute 'Created 0x10'): March 4, 2025, 10:15 AM, file path C:\Users\ktams\Desktop\Confidential\password.docx . File 2 details: - Filename: password.LNK - Extension: .LNK - Creation timestamp (recorded in the NTFS MFT record, attribute 'Created 0x10'): March 4, 2025, 1:10 AM. File source path of lnk is ; C:\\Users\\ktams\\AppData\\Roaming\\Microsoft\\Windows\\Recent\\password.lnk . Also relationship between them is shown as inside the properties of lnk there is local path C:\Users\ktams\Desktop\Confidential\password.docx  and show the relationship as password.lnk is lnk file of password.docx 

Here is the JSON-LD output based on your scenario: -- at one time valid json ld no validation input required

```json
Copy
Edit
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
      "@id": "kb:file-4d2f4567-bf34-48a3-b23c-91cf1b2a7e90",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-8a3c4123-e78d-4bcf-9f31-2a6f17c5e456",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "password.docx",
          "uco-observable:filePath": "C:\\Users\\ktams\\Desktop\\Confidential\\password.docx",
          "uco-observable:extension": ".docx",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-04T10:15:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:file-7c4a6789-df12-4e2d-94b3-b12f8e45a9c0",
      "@type": "uco-observable:File",
      "uco-core:hasFacet": [
        {
          "@id": "kb:filefacet-2f14c789-b23d-4a1f-88e2-7b1d2a5e89c4",
          "@type": "uco-observable:FileFacet",
          "uco-observable:fileName": "password.LNK",
          "uco-observable:filePath": "C:\\Users\\ktams\\AppData\\Roaming\\Microsoft\\Windows\\Recent\\password.lnk",
          "uco-observable:extension": ".LNK",
          "uco-observable:observableCreatedTime": {
            "@type": "xsd:dateTime",
            "@value": "2025-03-04T01:10:00Z"
          }
        }
      ]
    },
    {
      "@id": "kb:relationship-6d5f1234-b78a-49e3-88d4-3c2b9a5f1e78",
      "@type": "uco-observable:ObservableRelationship",
      "uco-core:source": { "@id": "kb:file-7c4a6789-df12-4e2d-94b3-b12f8e45a9c0" },
      "uco-core:target": { "@id": "kb:file-4d2f4567-bf34-48a3-b23c-91cf1b2a7e90" },
      "uco-core:kindOfRelationship": "Shortcut_To",
      "uco-core:isDirectional": true
    }
  ]
}
Would you like to make any changes?
