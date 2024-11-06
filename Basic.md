# 🔴 Zkopírování repository z DevOps

    clone repository z master větve a vytvoření projektu ve VSCode
![alt text](./images/image-3.png)
---
# 🔴 Stáhnutí symbolů 
    1. stažení extension - AL Language extension for Microsoft Dynamics 365 Business Central
    je duležitá pro build, intellisense, ALGO, downloadSymbols
![alt text](./images/image-2.png)
---
    2. použít příkaz download symbols
![alt text](./images/image-4.png)
---
    3. automaticky se vytvoří launch.json
---
## 🟡 Popis launch.json
```json
    {
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Chvalis-DEV",
            "request": "launch",
            "type": "al",
            "environmentType": "Sandbox",
            "server": "https://businesscentral.dynamics.com/66765fa5-0273-49e1-b190-b8a7f3e60b9a/DEV",
            "serverInstance": "BC",
            "authentication": "UserPassword",
            "startupObjectId": 22,
            "startupObjectType": "Page",
            "breakOnError": "All",
            "launchBrowser": true,
            "enableLongRunningSqlStatements": true,
            "enableSqlInformationDebugger": true,
            "tenant": "66765fa5-0273-49e1-b190-b8a7f3e60b9a",
            "usePublicURLFromServer": true,
            "schemaUpdateMode": "ForceSync",
            "startupCompany": "default"
        }
    ]
}
```
## 🟡 Popis app.json

# 🔴 Nástroje před vytvoření základních objektů 
---
## 🟡 Namespace
   - slouží k organizace kódu do určených skupin, abych předešli konfliktů s názvy objektů
   - musí být nazačátku každeho custom objektu
   - intelliSense automaticky generuje using

```AL
    namespace Seyfor.Chvalis.Sales;

    using Microsoft.Pricing.PriceList;
```

## 🟡 Vytváření pomocí snippet
    stažení extension - waldos CRS AL language ext
        - pro rychlejší vytvoření objektů 
        - přiklad snippet ttablewaldo, tpagewaldo 
![alt text](./images/image-5.png)

## 🟡 Číslování objektů
### 🟢 více možností jak udržovat pořádek v číslování objektů
    1. zabudované číslování od MC
        - nevýhoda při spolupráce více programátorů
    extension pro usnadnění - AL SOL UTILS 
     - přehled čísel všech objektů v app
![alt text](./images/image-7.png)

![alt text](./images/image-6.png)

    2. AL Object Ninja
        - nutná extension AL Object ID Ninja
        - nutné nastavení authorizačního json
![alt text](./images/image-8.png)
```json
{
  // This is the authorization key for all back-end communication. DO NOT MODIFY OR DELETE THIS VALUE!
  "authKey": "authKey",
  "idRanges": [
    {
      "from": 51000,
      "to": 51999,
      "description": "Sales"
      
    },
    {
      "from": 52000,
      "to": 52999,
      "description": "Purchases"
      
    }
  ]
}
```
    3. externí programy
        - např. projekt ALEF - Excel list 

## 🟡 Překlady
    překlady se nachází v projektu pod složkou Translation
        - g.xlf - generuje se při buildění - každý caption a label
        -.cs-CZ.xlf - generuje se z g.xlf souboru
💡 pokud nechci label / caption překládat, musím přidat Locked = true;
```javascript
        Pwd: Label 'Seyfor105', Locked = true;        
```
### 🟢 Nástroje pro práci s překlady
1. AL SOL Utils
    - nejčastejší použití pro generování překladových souborů z g.xlf
    - Postup:
        1.  build app - pro aktualizování g.xlf
        2.  použití příkazu ![alt text](./images/image-11.png) 
        3.  extension označí chybějící překlady
        4. pomocí zkratky CTL+T nad označeným polem, doplním překlad 
 
    ![alt text](./images/image-6.png)
2. NAB AL Tools
        - pro přeložení ze souboru ve kterém již překlady existují - lze použít i AL SOL Utils
![alt text](./images/image-9.png)

   

## 🟡 Others VSCode extension
- AL SOL Utils  - [link](https://solitea.sharepoint.com/sites/P-SCDL-DYN365ERP/Tools/Forms/AllItems.aspx?id=%2Fsites%2FP%2DSCDL%2DDYN365ERP%2FTools%2FAL%5FSOL%5FUTILS&p=true&ga=1)

    
# 🔴 Základní objekty 
---
## 🟡 Tables
### 🟢 table properties
- TableType - Normal (výchozí), Temporary
    - Temp vs Normal  - temporary většinou slouží k dočasnému zpracování velkých objemů dat bez vlivu na výkon databáze
- DataClassification 
### 🟢 příklady polí
```C#
// Int pole
        field(1; "TestField"; Integer)
        {
            Caption = 'MyField';
            ToolTip = 'specifiation';
            DataClassification = CustomerContent;
        }

// tableRelation
        field(3; "TestTableRelation"; Code[10])
        {
            Caption = 'TestTableRelation';
            DataClassification = CustomerContent;
            TableRelation = if (EnumTest = filter(EnumTest::Customer)) Customer else
            if (EnumTest = filter(EnumTest::Vendor)) Vendor else
            if (EnumTest = filter(EnumTest::"Purchase Invoice")) "Purch. Inv. Header" else
            if (EnumTest = filter(EnumTest::"Sales Cr. Memo")) "Sales Cr.Memo Header" else
            if (EnumTest = filter(EnumTest::"Purchase Cr. Memo")) "Purch. Cr. Memo Hdr.";

        }
    
// flowfield
        field(4; TestFlowField; Code[20])
        {
            Caption = 'TestFlowField';
            FieldClass = FlowField;
            Editable = false;
            CalcFormula = lookup("Sales Header"."No." where("Dimension Set ID" = field(TestField)));
        }
``` 
### 🟢 Field triggers
- OnLookup 
- OnValidate 
### 🟢 FlowField types
| FlowField type 	|                 Field type                	|                             Description                            	|   	|   	|
|:--------------:	|:-----------------------------------------:	|:------------------------------------------------------------------:	|---	|---	|
| Sum            	| Decimal, Integer, BigInteger, or Duration 	| The sum of a specified set in a column in a table.                 	|   	|   	|
| Average        	| Decimal, Integer, BigInteger, or Duration 	| The average value of a specified set in a column in a table.       	|   	|   	|
| Exist          	| Boolean                                   	| Indicates whether any records exist in a specified set in a table. 	|   	|   	|
| Count          	| Integer                                   	| The number of records in a specified set in a table.               	|   	|   	|
| Min            	| Any                                       	| The minimum value in a column in a specified set in a table.       	|   	|   	|
| Max            	| Any                                       	| The maximum value in a column in a specified set in a table.       	|   	|   	|
| Lookup         	| Any                                       	| Looks up a value in a column in another table.                     	|   	|   	|
---
### 🟢 Keys
-maximální počet 40

#### Primary key
Primární klíče hrají zásadní roli při jednoznačné identifikaci každého záznamu v tabulce. Definováním primárního klíče vývojáři zajišťují integritu dat a usnadňují rychlou manipulaci s daty a jejich vyhledávání.
#### Secondary key
Sekundární klíče naproti tomu vytvářejí indexy v jazyce SQL, které umožňují efektivní vyhledávání a získávání dat. Lze je definovat jak v table objektech, tak v table extension. Sekundární klíče navíc nabízejí další úroveň integrity dat tím, že vynucují jedinečnost v konkrétních polích.
#### Clustered Property
Clusterový index určuje fyzické pořadí ukládání dat na disku, což usnadňuje rychlejší přístup a vyhledávání. 
#### Unique Property
Toto omezení zajišťuje, že hodnoty v polích klíče zůstanou jedinečné, a zabraňuje tak duplikaci dat.
```C#
    keys
    {
        key(PK; "TestField")
        {
            Clustered = true;
        }
        key(SecondaryKey; "EnumTest", TestTableRelation)
        {
        }
    }
```
### 🟢table trigger
- OnDelete
- OnInsert
- OnModify
- OnRename
## 🟡 TableExts

## 🟡 Pages
### 🟢 Field triggers
- OnLookup - Multiselect, Drop-down list, Lookup list
## 🟡 PageExts
## 🟡 Codeunits
## 🟡 Reports
## 🟡 Queries
## 🟡 Enums
- nahradily OptionMembers 
- stavající enums se dají rozšiřovat pomocí extension, pokud je dovoleno
```C#
// příklad Enum
enum 51000 TestEnum
{
    Extensible = true;

    value(0; Customer)
    {
    }
    value(1; Vendor)
    {
    }
    value(2; "Purchase Invoice")
    {
    }
    value(3; "Sales Cr. Memo")
    {
    }
    value(4; "Purchase Cr. Memo")
    {
    }
}
```
---
```C#
// příklad EnumExtension
enumextension 51000 TestEnumExt extends "Attachment Document Type"
{
    value(51000; PDF)
    {
        Caption = 'PDF';
    }
}
```
## 🟡 PermissionSet
 ```C#
 //  příklad PermissionSet

permissionset 51001 "CHVL General"
{
    Assignable = true;
    ExcludedPermissionSets = "CHVL Sales VIP";

    IncludedPermissionSets = "CHVL SalesPermission";

    Permissions = table TestTable = X,
                tabledata TestTable = RIMD;
}
```
---
    při vytváření permission setů většinou využíváme nový objekt, ale je možné použít i permissionSetExt, zde je ale možné použít pouze exclude permission sets

## 🟡 EventSubscribers


# 🔴 Pokročilé témata
---
## 🟡 Error handling
## 🟡 Transaction isolations and tri-state locking

#### History
    Since its port to SQL server from native database, Navision used to implement a pessimistic locking,
     enforced by the application, with Serialize isolation lavel for all transactions that were accessing the same resource after a Modify, Insert or Delete.

     With a specific platform hotfix for Dynamics Nav 5.0 SP1 and from Dynamics NAV 2009 SP1, Microsoft slightly open to less locking scenarios where it was possible to opt for Repeatable Read isolation level instead. And this became the transaction isolation level up to now.

     From Dynamics 365 Business Central 2023 Wave 2 (version 23.x), Microsoft is finally opening to enable Read Committed as main transaction isolation level for object resource concurrency. This has also been called and mostly known as tri-state locking.

#### Tri-state locking
    Tri-state locking is in feature preview with Dynamics 365 Business central 2023 Wave 2 (version 23.x)
    and it is reversible (it could be turned on and off at will). In newly created environments with 23.0 and onwards, this feature is turned ON by default while environment upgraded from previous versions it is turned off by default

![alt text](./images/image.png)

## 🟡 DotNet changes / Streams BC
## 🟡 Interface



