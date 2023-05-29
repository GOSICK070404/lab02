## Laboratory work II by Polyakov Andrey IU8-21

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [ ] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [ ] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [ ] 3. Ознакомиться со ссылками учебного материала
- [ ] 4. Выполнить инструкцию учебного материала
- [ ] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=<имя_пользователя>
$ export GITHUB_EMAIL=<адрес_почтового_ящика>
$ export GITHUB_TOKEN=<сгенирированный_токен>
$ alias edit=nano
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```sh
$ mkdir ~/.config
mkdir: cannot create directory ‘/home/kali/.config’: File exists
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /home/kali/GOSICK070404/workspace/projects/lab02/.git/

$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
[hub]
        protocol = https
[user]
        name = GOSICK070404
        email = poliakovam@ya.ru
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
fatal: couldn't find remote ref master
$ touch README.md
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
 
$ git add README.md
$ git commit -m"added README.md"
master (root-commit) 79906cb] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md

$ git push origin master
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 222 bytes | 74.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/GOSICK070404/lab02/pull/new/master
remote: 
To https://github.com/GOSICK070404/lab02.git
 * [new branch]      master -> master

```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin master
From https://github.com/GOSICK070404/lab02
 * branch            master     -> FETCH_HEAD
Already up to date.

$ git log
commit 79906cbfdf5abaf74615d60e22aa79f17398cd63 (HEAD -> master, origin/master)
Author: GOSICK070404 <poliakovam@ya.ru>
Date:   Mon May 29 13:16:17 2023 -0400

    added README.md
                          
```

```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
$ edit README.md
```

```sh
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        examples/
        include/
        sources/

no changes added to commit (use "git add" and/or "git commit -a")

$ git add .
$ git commit -m"added sources"
[master 115ee7f] added sources
 5 files changed, 33 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp

$ git push origin master
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Enumerating objects: 12, done.
Counting objects: 100% (12/12), done.
Delta compression using up to 2 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (10/10), 919 bytes | 229.00 KiB/s, done.
Total 10 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/GOSICK070404/lab02.git
   79906cb..115ee7f  master -> master

```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
Cloning into 'tasks/lab02'...
remote: Enumerating objects: 96, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 96 (delta 0), reused 1 (delta 0), pack-reused 93
Receiving objects: 100% (96/96), 1.29 MiB | 531.00 KiB/s, done.
Resolving deltas: 100% (28/28), done.
                                      
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I
1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
```sh
┌──(kali㉿kali)-[~]
└─$ cd ~/GOSICK070404/workspace/
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace]
└─$ source scripts/activate 
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace]
└─$ mkdir ~/.config
mkdir: cannot create directory ‘/home/kali/.config’: File exists
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace]
└─$ mkdir projects/lab02_homework                              
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace]
└─$  cd projects/lab02_homework
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint: 
hint:   git config --global init.defaultBranch <name>
hint: 
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint: 
hint:   git branch -m <name>
Initialized empty Git repository in /home/kali/GOSICK070404/workspace/projects/lab02_homework/.git/
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git config --global user.name ${GITHUB_USERNAME}
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git config --global user.email ${GITHUB_EMAIL}
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git config -e --global 
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git remote add origin https://github.com/GOSICK070404/lab02dz    
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git pull origin master         
fatal: couldn't find remote ref master
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ touch README.md
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md

nothing added to commit but untracked files present (use "git add" to track)
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git add README.md
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m "added README.md"
[master (root-commit) d774c8f] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git push origin master       
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 222 bytes | 222.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'master' on GitHub by visiting:
remote:      https://github.com/GOSICK070404/lab02dz/pull/new/master
remote: 
To https://github.com/GOSICK070404/lab02dz
 * [new branch]      master -> master
  ```
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ mkdir sources
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ cat > sources/hello_world.cpp <<EOF
> #include <iostream>
> using namespace std;
> int main(){
> cout<<"Hello, world!";
> return 0;
> }
heredoc> EOF
```
4. Добавьте этот файл в локальную копию репозитория.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git add sources/hello_world.cpp
```
5. Закоммитьте изменения с *осмысленным* сообщением.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m"added hello_world.cpp"
[master 7c56502] added hello_world.cpp
 1 file changed, 6 insertions(+)
 create mode 100644 sources/hello_world.cpp
```
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ edit sources/hello_world.cpp
```
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m"fixed hello_world.cpp"
[master 2e6fcfb] fixed hello_world.cpp
 1 file changed, 1 insertion(+), 1 deletion(-)
```
8. Запуште изменения в удалёный репозиторий.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$  git push origin master 
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 2 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (8/8), 845 bytes | 845.00 KiB/s, done.
Total 8 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/GOSICK070404/lab02dz
   d774c8f..2e6fcfb  master -> master
```
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$  git checkout -b patch1
Switched to a new branch 'patch1'
```
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ edit sources/hello_world.cpp
```
3. **commit**, **push** локальную ветку в удалённый репозиторий.
```sh
──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m"fixed hello_world.cpp"
On branch patch1
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   sources/hello_world.cpp

no changes added to commit (use "git add" and/or "git commit -a")
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git add sources/hello_world.cpp 
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m"fixed hello_world.cpp"
[patch1 7e7ef5d] fixed hello_world.cpp
 1 file changed, 1 deletion(-)
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$  git push origin patch1
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 2 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 371 bytes | 371.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/GOSICK070404/lab02dz/pull/new/patch1
remote: 
To https://github.com/GOSICK070404/lab02dz
 * [new branch]      patch1 -> patch1
     ```                                                                       
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ edit sources/hello_world.cpp
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git add sources/hello_world.cpp 
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m"added comments to hello_world.cpp"
[patch1 b59f637] added comments to hello_world.cpp
 1 file changed, 1 insertion(+)
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git push origin patch1
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 2 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 444 bytes | 444.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/GOSICK070404/lab02dz
   7e7ef5d..b59f637  patch1 -> patch1
```
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git pull origin main
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), 1.19 KiB | 1.19 MiB/s, done.
From https://github.com/GOSICK070404/lab02dz
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> origin/main
```
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$  git log        
commit b59f637efaa6c3e43d7867cfb4a689d0b7586a1f (HEAD -> patch1, origin/patch1)
Author: GOSICK070404 <poliakovam@ya.ru>
Date:   Mon May 29 14:48:29 2023 -0400

    added comments to hello_world.cpp

commit 7e7ef5d864197165cacd42b873edf7ec61f6baf0
Author: GOSICK070404 <poliakovam@ya.ru>
Date:   Mon May 29 14:43:38 2023 -0400

    fixed hello_world.cpp

commit 2e6fcfb0cdce19ca8f7c35609612b06a208c24ce (origin/master, master)
Author: GOSICK070404 <poliakovam@ya.ru>
Date:   Mon May 29 14:39:43 2023 -0400

    fixed hello_world.cpp

commit 7c56502e9006ac8a72fccc39b645c72e4271548d
Author: GOSICK070404 <poliakovam@ya.ru>
Date:   Mon May 29 14:35:47 2023 -0400

    added hello_world.cpp

commit d774c8fd52061214662995f62d3915a252e22b78
Author: GOSICK070404 <poliakovam@ya.ru>
Date:   Mon May 29 14:33:24 2023 -0400

    added README.md
```
12. Удалите локальную ветку `patch1`.
```sh
──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git branch --delete patch1 
error: Cannot delete branch 'patch1' checked out at '/home/kali/GOSICK070404/workspace/projects/lab02_homework'
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git checkout master 
Switched to branch 'master'
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git branch --delete patch1 
error: The branch 'patch1' is not fully merged.
If you are sure you want to delete it, run 'git branch -D patch1'.
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git branch -D patch1 
Deleted branch patch1 (was b59f637).
```                                                                                      

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git checkout -b patch2
Switched to a new branch 'patch2'
```
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ clang-format -i --style=Mozilla sources/hello_world.cpp
Command 'clang-format' not found, but can be installed with:
sudo apt install clang-format
Do you want to install it? (N/y)y
sudo apt install clang-format
[sudo] password for kali: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package clang-format
```
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git add sources/hello_world.cpp 
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m"changed code-style"
On branch patch2
nothing to commit, working tree clean
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git push origin patch2 
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
remote: 
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/GOSICK070404/lab02dz/pull/new/patch2
remote: 
To https://github.com/GOSICK070404/lab02dz
 * [new branch]      patch2 -> patch2
```
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ edit sources/hello_world.cpp
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m "new comment"
On branch patch2
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   sources/hello_world.cpp

no changes added to commit (use "git add" and/or "git commit -a")
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git add .
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git commit -m "new comment"
[patch2 eb5cb23] new comment
 1 file changed, 1 insertion(+), 1 deletion(-)
                                                                                                                    
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git push origin patch2 
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Enumerating objects: 7, done.
Counting objects: 100% (7/7), done.
Delta compression using up to 2 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 369 bytes | 369.00 KiB/s, done.
Total 4 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/GOSICK070404/lab02dz
   2e6fcfb..eb5cb23  patch2 -> patch2
```
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git pull --rebase origin patch2
From https://github.com/GOSICK070404/lab02dz
 * branch            patch2     -> FETCH_HEAD
Already up to date.
```
7. Сделайте *force push* в ветку `patch2`
```sh
┌──(kali㉿kali)-[~/GOSICK070404/workspace/projects/lab02_homework]
└─$ git push origin patch2 --force
Username for 'https://github.com': GOSICK070404
Password for 'https://GOSICK070404@github.com': 
Everything up-to-date
```
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2021 The ISC Authors
```
