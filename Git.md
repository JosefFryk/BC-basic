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
    - TODO:
3. VSCode command pallet - TODO:
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

## 🟡 Clone changes

### 🟢 Setting for Source control
---
#### Ingoing/Outgoing source control
- od Tomáše
Koho štve „Incoming/Outgoing“ graf v „Source Control“, tak to lze vypnout (zpomaluje to).
Viz nastavení „scm.showHistoryGraph“.
- ![alt text](/images/IngoinOutgoin1.png)
- ![alt text](/images/IngoinOutgoin2.png)
- ![alt text](/images/IngoinOutgoin3.png)
---
#### Source control - only modified objects
- Setting "git.openDiffOnClick": false and "scm.defaultViewMode": "tree"
## 🟡 First commit

## 🟡 View History using Azure Repos web interface
## 🟡 Working with branches

## 🟡 Tagging a release

## 🟡 Managing repository

## 🟡 Managing Pull request

## 🟡 Conflicts

## 🟡 Cherrypicking
