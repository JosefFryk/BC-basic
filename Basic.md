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
### Tables
### TableExts
### Pages
### PageExts
### Codeunits
### Reports
### Queries




