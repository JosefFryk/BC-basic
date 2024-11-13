# Azure DevOps: Git Basics
## 🟡 Azure Repos
![alt text](/images/AzureRepos.png)
 - Pomáhá sledovat změny v codebase
- Udržuje historii vaší codebase, kdo provedl změny, jaké změny byly provedeny, proč byly změny provedeny atd.
- Pomáhá vám udržovat pořádek
- Dává vám možnost vrátit změny zpět podle potřeby
## 🟡 GIT vs TFVC
![alt text](/images/GitTFVC.png)
### 🟢 GIT
Git je nejpoužívanější distribuovaný systém pro správu verzí. Umožňuje vývojářům stáhnout celý repozitář kódu lokálně se všemi verzemi a provádět změny vzdáleně/offline. Následně lze změny synchronizovat se vzdáleným serverem.

K interakci se systémem Git můžete využít klienty, jako je Git for Windows, VSCode atd. Git poskytuje systém správy verzí, ale k hostování codebase (repozitářů) potřebujeme hostingovou službu.Jako jsou například GitHub, Azure Repos, Bitbucket, Gitlab atd.

### 🟢TFVC
Dalším typem systému správy verzí je Team Foundation Version Control, centralizovaná správa verzí. V systému TFVC se lokálně stahuje pouze jedna verze codebase a historická data se udržují na centrálním serveru. TFVC můžete hostovat pomocí hostingových služeb, jako je Perforce, SVC, Azure Repos atd.

Zamykání jednotlivých souborů při změně.

## 🟡 Connect Visual Studio to Git
![alt text](/images/CloneRepo.png)
1. HTTPS - připojit se pomocí URL, které nám Repo nabízí
    - otevřeme terminál v VS Code
    - změníme aktuální pracovní adresář na místo, kam chceme klonovaný adresář umístit
    - git clone <Your URL>
2. použít IDE - button Clone in VS Code
    1. automaticky nám spustí VSCode
    2. vybere místo uložení
    3. otevřeme adresář přes workspace
3. VSCode command pallet
4. SHH - připojení pomocí public/private klíče 

## 🟡 Branches
### 🟢 core concepts
1. "HEAD" branch
    - v jednu chvíli můžeme mít aktivní pouze jednu branch 
    - ![alt text](/images/terminalMain.png)
    - ![alt text](/images/UImain.png)
2. Local and Remote
    - většinu času pracujeme s local branches
    - ![alt text](/images/localRemotes.png)

### 🟢 new branch
```
    git branch <name>
    git branch <name> <commit>
```
### 🟢 switching branch
```
    git switch <name of branch to switch>
```
### 🟢 rename branch
#### local branches
```
    git branch -m <new name>

    //non HEAD branch
     git branch -m <oldName> <newName>
```
#### remotes branches
- lepší smazat a vytvořit novou
```
git push origin --delete <old name>

git push -u origin <new name>
```
### 🟢 publishing branches
- public local branches to share
```
git push -u origin <local branch>
```
### 🟢 Tracking branches
![alt text](/images/trackingBranches.png)
```
git brach --track <new branch> origin/<base-branch>
//nebo
git checkout --track origin/<base branch>
```
- lehčí synchronizace mezi local a remote branch
- DevOps PR rovnou nabídne změny z local branch při publikování

Synchronizace local a remote branch
- ![alt text](/images/GitStatus.png)
- ![alt text](/images/UITracking.png)

- rozdíl mezi bez a s tracking
- ![alt text](/images/trackingDiff.png)
### 🟢 Pulling + Pushing branches
```
git pull
git push

git branch -v
```
- při vytváření pomocí UI tracking je automatické

### 🟢 Deleting branches
```
//local branch
git branch -d <branch name>
```
- většina větví je určená ke smazání
- pokud chceme smazat local branch s úpravami, které nejsou jidne musíme použím -f
- při smazání je dobré zkontrolovat, které větve mají společný tracking, popřípadě smazat
```
//remote branch
git push origin --delete <branch name>
```

### 🟢 Merging branches
```
//1. zmenit head branch na tu která obdrží změny
git switch <branch receiver>

//2. použít příkaz merge s názvem větve, kde se změny nachází
git merge <branch with changes>
```
- merging vyvola merge commit, musíme poskytnout commit message
![alt text](/images/MergingBranches.png)
### 🟢 Rebasing branches
- stejné jako merging branches, s tím,že historie je pak přímá linka
![alt text](/images/RebasingBranches.png)

### 🟢 Comparing branches
```
git log <main branch>..<compare branch>
```
- zobrazí rozdíl commitů mezi dvěmi větvy



## 🟡 Source control
---
### 🟢 Source Control changes / stage
![alt text](/images/StageChanges.png)
![alt text](/images/UIStage.png)
- v naší praxi je při rozdělování commitů trochu problém s překlady
```
// add all to stage
    git add .
    
// add file
    git add <fileName>

// check diffrence between stage and unstage
    git diff

// bonus - přidání části kódu ze souboru - moc se nepoužívá
git add -p <FileName>
```
### Commit
- pro vytvoření nového commitu ze staged kódu
```
git commit
```
### Commit message
- Commit msg se liší projekt od projektu 
- stejný začátek je číslo tasků, pro který je úprava
- ![alt text](/images/commitMsg.png)
- ![alt text](image-2.png)
### 🟢 Git Stash
- git stash poskytuje dočasné uschování změn, ke kterým se později můžeme vrátit bez toho aniž by jsme museli změny commitnout
- nové soubory automaticky nebudou umístěny do stashe // pokud je potřeba musí se použít parametr -u
```
//uloží změny do stash
git stash 

//odstrani poslední stash a aplikuje je do aktualniho kódu
git stash pop

// aplikování změn do kódu bez smazání stash -- pro více větví např.
git stash apply

// zobrazit stash list
git stash list
```
#### stejné příkazy platí i pro UI || Source control -> ... -> stash
![alt text](/images/stash.png)

### 🟢 Pull Request
- jsou poskytnuty Azure Repos, nejsou součásti gitu
- ![alt text](/images/PRGraph.png)

### 🟢 Settings Source Control
#### 🔴 Git Graph
- pro přehlednější práci s Git - filtrování
![alt text](/images/GitGraph.png)
---
#### 🔴 Ingoing/Outgoing source control
- od Tomáše
Koho štve „Incoming/Outgoing“ graf v „Source Control“, tak to lze vypnout (zpomaluje to).
Viz nastavení „scm.showHistoryGraph“.
- ![alt text](/images/IngoinOutgoin1.png)
- ![alt text](/images/IngoinOutgoin2.png)
- ![alt text](/images/IngoinOutgoin3.png)
---
#### 🔴 Source control - only modified objects
- Setting "git.openDiffOnClick": false and "scm.defaultViewMode": "tree"

## 🟡 Git Tag
- jsou reference commitu, na který můžeme použit příkazy checkout, diff nebo z nich udělat archiv
- nejčastejší použití je archiv pro release kódu do produkce / testu, před přidáním nových commitů
![alt text](/images/GitTag.png)

## 🟡 Merge Conflicts
1. proč nastávájí konflikty
![alt text](/images/whyMergeConflict.png)
![alt text](/images/mergeConflict1.png)


## 🟡 Cherrypicking
- aplikování změn(commit) z jedné branch do druhé branch
- např. ALEF master vs UAT větev 
- pokud víme, že nenastanou konflikty při je lehčí použít DevOps UI 
### DevOps CherryPick
1. Na kartě commitu vybereme cherrypick
- ![alt text](/images/cherryPick1.png)
2. DevOps nám automaticky nabídne nově vytvořenou větev podle target branch
- ![alt text](/images/CherryPick2.png)


- video s cherryPick tematikou ALEF UAT 
[Sharepoint Solitea](https://solitea.sharepoint.com/sites/P-CDL-00027/_layouts/15/stream.aspx?id=%2Fsites%2FP%2DCDL%2D00027%2FRealizace%2FVideoz%C3%A1znamy%2F%5FSeyfor%20intern%C3%AD%20prezentace%2F2024%2D05%2D05%2DNasazov%C3%A1n%C3%AD%20UAT%2FALEF%20BC%20%2D%20UAT%20%2D%20nasazov%C3%A1n%C3%AD%20%C3%BAprav%2D20240604%5F090202%2DZ%C3%A1znam%20sch%C5%AFzky%2Emp4&referrer=StreamWebApp%2EWeb&referrerScenario=AddressBarCopied%2Eview%2E2fefc0de%2D9113%2D40e1%2D9190%2Db24f5a9e1943)