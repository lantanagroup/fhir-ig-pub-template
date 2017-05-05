# fhir-ig-pub-template
Templates for the FHIR IG Publisher. Uses jquery and jquery-ui to create tabbed HTML output

## Templates

| Name | Purpose |
|--|--|
| instance-template-base.html | Used for instances that are not StructureDefinition (ex: examples instances, like Composition/C-CDA-Referral-Note-Example) |
| instance-template-format.html | Used on each resource for different formats (ex: XML and JSON) |
| instance-template-sd.html | Used for StructureDefinition resources |

## Example Control File

```
{
  "tool": "jekyll",
  "paths": {
    "resources": [
      "resources"
    ],
    "pages": "pages",
    "temp": "temp",
    "output": "output",
    "qa": "qa",
    "specification": "http://hl7-fhir.github.io/"
  },
  "defaults": {
    "Any": {
      "template-format": "instance-template-format.html",
      "template-base": "instance-template-base.html"
    },
    "StructureDefinition": {
      "template-base": "instance-template-sd.html"
    }
  },
  "canonicalBase": "AAAA",
  "source": "ImplementationGuide/BBBB.xml",
  "sct-edition": "http://snomed.info/sct/731000124108",
  "special-urls": [],
  "resources": {
    "StructureDefinition/XXXX": {
      "base": "StructureDefinition-XXXX.html"
    },
    "ValueSet/YYYY": {
      "base": "ValueSet-YYYY.html"
    },
    "Composition/ZZZZ": {
      "base": "Composition-ZZZZ.html"
    }
  }
}
```

Each of the resources listed should be placed in a separate "resources" directory. You can optionally categorize the resources into sub-directories based on the resource type (ex: one directory for "StructureDefinition", another for "Composition", etc.)

## Additional Files

This template uses additional files in the pages/_includes directory to populate the home page. These files will need to be created for each implementation guide that uses this set of templates.

| File Name | Description |
|--|--|
| pages/_includes/description.html | Homepage > "Overview" tab, at the top of the tab |
| pages/_includes/authors.html | Homepage > "Overview" tab, below the description |
| pages/_includes/overview.html | Homepage > "Overview" tab, below the authors |
| pages/_includes/resources.html | Homepage > "Resources" tab |
| pages/_includes/valuesets.html | Homepage > "Value Sets" tab |
| pages/_includes/codesystems.html | Homepage > "Code Systems" tab |
| pages/_includes/extensions.html | Homepage > "Extensions" tab |

## Additional Data

This template uses an extra data (JSON) file in the pages/_data directory called "examples.json" to determine which examples are associated with each StructureDefinition.

Example of pages/_data/examples.json:

```
{
  "AAAA": {
    "examples": [
      {
        "type": "Composition",
        "id": "XXXX-Example"
      }
    ]
  },
  "BBBB": {
    "examples": [
      {
        "type": "Composition",
        "id": "YYYY-Example"
      }
    ]
  }  
}
```

In the above example, AAAA and BBBB represents the id of a StructureDefinition, and XXXX and YYYY represent the id of an example instance included in the package.

## Run the IG Publisher

1. Download the FHIR IG Publisher JAR from http://build.fhir.org/downloads.html The direct link to the FHIR IG Publisher JAR is: http://build.fhir.org/org.hl7.fhir.igpublisher.jar
2. Place the JAR file in the same directory as the other files extracted from the FHIR Build package
3. Create a control file (see above)
4. Create the additional files (see above)
5. Create the additional data file (see above)
6. Add all your resources to the "resources" directory.
7. Update the RunIgPublisherCmd.bat file to reference the name of the control file.
9. Run one of the "RunXXX.bat" batch files.