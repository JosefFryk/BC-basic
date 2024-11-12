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
- při vytváření pomocí UI tracking je automatické
## 🟡 Clone changes

### 🟢 Setting for Source control


## 🟡 First commit

## 🟡 View History using Azure Repos web interface

## 🟡 Working with branches

## 🟡 Tagging a release

## 🟡 Managing repository

## 🟡 Managing Pull request

## 🟡 Conflicts

## 🟡 Cherrypicking
