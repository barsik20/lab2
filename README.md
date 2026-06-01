# Лабораторная работа №02
## Работа с Git и GitHub

---

## Часть 1.
1.1. Создание пустого репозитория на GitHub

На сайте github.com создан новый репозиторий lab2h без README, .gitignore.

1.2. Настройка Git и создание локальной копии


```sh 
git config --global user.name "barsik20"
git config --global user.email "bars.070620077777@gmail.com"
cd barsik20/workspace/projects
mkdir lab2
cd lab2
git init
```

1.3. Первый коммит (README.md)
```sh 
echo "Home task" > README.md
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/barsik20/lab2.git
git push -u origin main
```
<details> <summary>📋 Вывод git push</summary>
  <pre>
Username for 'https://github.com': barsik20
Password for 'https://barsik20@github.com':
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 222 bytes | 222.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/barsik20/lab2.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
  </pre>
 </details>

1.4. Создание программы hello_world.cpp (плохой стиль)
```sh 
cat > hello_world.cpp <<EOF
#include <iostream>
using namespace std;
int main()
{
    cout << "Hello world!" << endl;
    return 0;
}
EOF
 ```

1.5. Добавление ввода имени пользователя
```sh 

cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

using namespace std;

int main()
{
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello world from " << name << endl;
    return 0;
}
EOF
```
Делаем git commit

1.6. Отправка изменений на GitHub и проверка истории
```sh
git push
```
Изменения отправлены в удалённый репозиторий.
<details> <summary>📋 Вывод git push</summary>
  <pre>
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 219 bytes | 219.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/barsik20/lab2.git
 * [new branch]      main -> main
branch 'main' set up to track 'origin/main'.
  </pre>
</details>

---
## Часть 2
2.1. Создание локальной ветки patch1
```sh
git checkout -b patch1
```
Создана новая ветка patch1 и выполнен переход на неё.


2.2. Исправление кода: удаление using namespace std
```sh
cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main()
{
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name;
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
EOF

```
2.3. Отправка ветки patch1 на GitHub
```sh
git push -u origin patch1
```
Ветка patch1 отправлена в удалённый репозиторий. После этого она доступна на GitHub.
<details> <summary>Вывод git push</summary>
  <pre>
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 436 bytes | 436.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
remote:
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/barsik20/lab2/pull/new/patch1
remote:
To https://github.com/barsik20/lab2.git
 * [new branch]      patch1 -> patch1

  </pre>
</details>

2.4. Добавление комментариев в код (ветка patch1)
```sh
cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main()
{
    // Request user name via standard input
    std::string name;
    std::cout << "Enter your name: ";
    std::cin >> name;
    
    // Output greeting with the entered name
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}
EOF

```
2.5. Обновление ветки main после слияния
```sh
git checkout main
git pull origin main
```
<details> <summary> Вывод git pull</summary>
<pre>
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (1/1), 913 bytes | 913.00 KiB/s, done.
From https://github.com/barsik20/lab2
 * branch            main       -> FETCH_HEAD
   b75783f..f673898  main       -> origin/main
Updating b75783f..f673898
Fast-forward
 hello_world.cpp | 14 ++++++++------
 1 file changed, 8 insertions(+), 6 deletions(-)

</pre>
</details>

2.6. Просмотр истории коммитов
```sh
git log --oneline --graph
```
<details> <summary>📋 Вывод git log --oneline после слияния patch1</summary>
<pre>
*   f673898 (HEAD -> main, origin/main) Merge pull request #1 from barsik20/patch1
|\
| * cb3ae08 (origin/patch1, patch1) Add documentation comments to the code
| * 101acfc Remove using namespace std and use std::...
|/
* b75783f Add user name input functionality
* 11c3fad Add hello world program with poor code style
* 9e07a8a first commit
</pre>
</details>

2.7. Удаление локальной ветки patch1
```sh
git branch -d patch1
```

## Часть 3.
3.1. Создание новой локальной ветки patch2
```sh
git checkout -b patch2
```
<details> <summary>📋 Вывод</summary>

```sh
Switched to a new branch 'patch2'
```
</details>

3.2. Изменение code style с помощью утилиты clang-format
Установка clang-format
```sh
sudo apt update
sudo apt install clang-format -y
```
Применение форматирования
```sh
clang-format -style=Mozilla -i hello_world.cpp
```
3.3. commit, push, создание pull-request patch2 -> master
```sh
git add hello_world.cpp
git commit -m "Apply Mozilla code style using clang-format"
git push -u origin patch2
```
<details> <summary>📋 Вывод коммита и push</summary>
<pre>
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 425 bytes | 425.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote:
remote: Create a pull request for 'patch2' on GitHub by visiting:
remote:      https://github.com/barsik20/lab2/pull/new/patch2
remote:
To https://github.com/barsik20/lab2.git
 * [new branch]      patch2 -> patch2
</pre>
</details>

3.4. В ветке main в удалённом репозитории изменим структуру кода

```sh
git checkout main

cat > hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main()
{
    // имя пользователя
    std::string name;
    // Ввод имени
    std::cout << "Enter your name: ";
    std::cin >> name;
    std::cout << "Hello world from @" << name << std::endl;
    return 0;
}return 0;
}
EOF
```

3.5. Убедиться, что в pull-request появились конфликты

После изменения комментариев в ветке main страница pull request на GitHub обновилась, и появилось сообщение:
«This branch has conflicts that must be resolved».

3.6. Локально выполнить pull + rebase
```sh
git checkout patch2
git fetch origin
git rebase origin/main
```

<details> <summary>Сообщение о конфликте</summary>
<pre>
From https://github.com/barsik20/lab2
 * branch            main       -> FETCH_HEAD
Auto-merging hello_world.cpp
CONFLICT (content): Merge conflict in hello_world.cpp
error: could not apply f5b3f6c... Apply Mozilla code style using clang-format
hint: Resolve all conflicts manually, mark them as resolved with
hint: "git add/rm <conflicted_files>", then run "git rebase --continue".
hint: You can instead skip this commit: run "git rebase --skip".
hint: To abort and get back to the state before "git rebase", run "git rebase --abort".
Could not apply f5b3f6c... Apply Mozilla code style using clang-format
</pre>
</details>
Чтобы исправить ошибки воспользуемся командой cat
<details> <summary>Исправление ошибки</summary>
  
```sh
 cat > hello_world.cpp <<'EOF'
```
Удаляем конфликтные маркеры и получаем следующий код

```sh
#include <iostream>
#include <string>

int main()
{
  // Твоё имя
  std::string name;
  std::cout << "Enter your name: ";
  std::cin >> name;

  // приветствие
  std::cout << "Hello world from " << name << std::endl;
  return 0;
}

```
</details>
После исправления конфликта

```sh
git add hello_world.cpp
git rebase --continue
```

3.7. Сделать force push в ветку patch2

``` sh
git push origin patch2 --force
```

Отправляет изменённую (после rebase) ветку patch2 в удалённый репозиторий, перезаписывая её историю.
<details> <summary>📋 Вывод force push</summary>
<pre>
Username for 'https://github.com': barsik20
Password for 'https://barsik20@github.com':
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 418 bytes | 418.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/barsik20/lab2.git
 + f5b3f6c...245bf9e patch2 -> patch2 (forced update)
</pre>
</details>
На GitHub нажата кнопка «Merge pull request», затем «Confirm merge». Ветка patch2 на GitHub удалена.


3.8. Локальное обновление main

```sh
git checkout main
git pull origin main
git log --oneline --graph --all
```
<details> <summary></summary> Окончательная история коммитов</summary>
<pre>

*   5392379 (HEAD -> main, origin/main) Merge pull request #2 from barsik20/patch2
|\
| * 245bf9e (origin/patch2, patch2) Apply Mozilla code style using clang-format
|/
* b3e59b0 Update comments with proper punctuation and grammar
*   f673898 Merge pull request #1 from barsik20/patch1
|\
| * cb3ae08 (origin/patch1) Add documentation comments to the code
| * 101acfc Remove using namespace std and use std::...
|/
* b75783f Add user name input functionality
* 11c3fad Add hello world program with poor code style
* 9e07a8a first commit
</pre>
</details>



