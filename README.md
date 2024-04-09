# Домашнее задание к занятию «Инструменты Git» - `Punin Sergey`

### Цель задания

В результате выполнения задания вы:

* научитесь работать с утилитами Git;
* потренируетесь решать типовые задачи, возникающие при работе в команде. 

### Инструкция к заданию

1. Склонируйте [репозиторий](https://github.com/hashicorp/terraform) с исходным кодом Terraform.
2. Создайте файл для ответов на задания в своём репозитории, после выполнения прикрепите ссылку на .md-файл с ответами в личном кабинете.
3. Любые вопросы по решению задач задавайте в чате учебной группы.

------

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
Ответьте на вопросы.

2. Какому тегу соответствует коммит `85024d3`?
3. Сколько родителей у коммита `b8d720`? Напишите их хеши.
4. Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.
5. Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).
6. Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.
7. Кто автор функции `synchronizedWriters`? 

*В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.*

---

## Ответ:
1. `Команда:`
   
   ```
    git log --oneline | grep '^aefea'
   
   ```
   
    `Итог:`
   
   ```
    aefead2207 Update CHANGELOG.md
   
   ```

2. `Команда:`

   ```
   git describe --tags 85024d3
   ```
   
   `Итог:`
   
   ```
   v0.12.23
   
   ```
3. `Команда:`

   ```
   git cat-file -p b8d720

   ```
   
   `Итог:`
   
   ```
   tree cec002aab630c8bc701cb85bc94e55e751cd2d8f
   parent 56cd7859e05c36c06b56d013b55a252d0bb7e158
   parent 9ea88f22fc6269854151c571162c5bcf958bee2b
   author Chris Griggs <cgriggs@hashicorp.com> 1579657548 -0800
   committer GitHub <noreply@github.com> 1579657548 -0800
   gpgsig -----BEGIN PGP SIGNATURE-----

    wsBcBAABCAAQBQJeJ6lMCRBK7hj4Ov3rIwAAdHIIAAWogFD+6nxgm7suNlJVqGv3
    iczwk1OySRvZiDhgJuaIEZMduudoIBnv7XStZsg5wQ7a0byh4iU6z7w6vVKPyj1e
    2KyTqwriHOYqDJ/pljIX92btLU+rXDP0DpnTg8WuMthqUJGh6q8OGorvlIHDwcdN
    DKZxKaLPaBYCD5nuYMyhuh9T6+4ayEN4zUbl5vLPN7XmvhSf4yDQ0H4UaR596qOo
    phaqODHglNLegdGwi+JaTtDSB/JO5zJNfn8OnuRgyhoplmKKlhBAEwS4muxjjkzD
    cUtFA+jkXaVpbfEh/dBRb3yB4W17jrxFDuDESjXKiU61bc8Fwa1JrfQAFlXczmY=
    =s9Hk
    -----END PGP SIGNATURE-----


   Merge pull request #23916 from hashicorp/cgriggs01-stable

   [Cherrypick] community linkssergey@Ubuntu:~/devops/terraform/terraform
   
   ```
4. `Команда:`

   ```
   git log v0.12.23..v0.12.24 --oneline
   
   ```
   `Итог:`
   
   ```
   33ff1c03bb (tag: v0.12.24) v0.12.24
   b14b74c493 [Website] vmc provider links
   3f235065b9 Update CHANGELOG.md
   6ae64e247b registry: Fix panic when server is unreachable
   5c619ca1ba website: Remove links to the getting started guide's old location
   06275647e2 Update CHANGELOG.md
   d5f9411f51 command: Fix bug when using terraform login on Windows
   4b6d06cc5d Update CHANGELOG.md
   dd01a35078 Update CHANGELOG.md
   225466bc3e Cleanup after v0.12.23 release

   ```

5. `Команда:`

   ```
   git log -S 'func providerSource('

   ```
   
   
   `Итог:`
   ```
   
   commit 8c928e83589d90a031f811fae52a81be7153e82f
   Author: Martin Atkins <mart@degeneration.co.uk>
   Date:   Thu Apr 2 18:04:39 2020 -0700

    main: Consult local directories as potential mirrors of providers

    This restores some of the local search directories we used to include when
    searching for provider plugins in Terraform 0.12 and earlier. The
    directory structures we are expecting in these are different than before,
    so existing directory contents will not be compatible without
    restructuring, but we need to retain support for these local directories
    so that users can continue to sideload third-party provider plugins until
    the explicit, first-class provider mirrors configuration (in CLI config)
    is implemented, at which point users will be able to override these to
    whatever directories they want.

    This also includes some new search directories that are specific to the
    operating system where Terraform is running, following the documented
    layout conventions of that platform. In particular, this follows the
    XDG Base Directory specification on Unix systems, which has been a
    somewhat-common request to better support "sideloading" of packages via
    standard Linux distribution package managers and other similar mechanisms.
    While it isn't strictly necessary to add that now, it seems ideal to do
    all of the changes to our search directory layout at once so that our
    documentation about this can cleanly distinguish "0.12 and earlier" vs.
    "0.13 and later", rather than having to document a complex sequence of
    smaller changes.

    Because this behavior is a result of the integration of package main with
    package command, this behavior is verified using an e2etest rather than
    a unit test. That test, TestInitProvidersVendored, is also fixed here to
    create a suitable directory structure for the platform where the test is
    being run. This fixes TestInitProvidersVendored.
   
      ```

6. `Команда:`
      
      ```
      
      git log -S'globalPluginDirs' --oneline

      ```
      
      `Итог:`
 
      ```
      65c4ba7363 Remove terraform binary
      125eb51dc4 Remove accidentally-committed binary
      22c121df86 Bump compatibility version to 1.3.0 for terraform core release (#30988)
      7c7e5d8f0a Don't show data while input if sensitive
      35a058fb3d main: configure credentials from the CLI config file
      c0b1761096 prevent log output during init
      8364383c35 Push plugin discovery down into command package
      
      ```
  
  7. `Команда:`
      
      ```
      git log -S'synchronizedWriters'  
      ```
      `Итог:`
      ```
      commit bdfea50cc85161dea41be0fe3381fd98731ff786
      Author: James Bardin <j.bardin@gmail.com>
      Date:   Mon Nov 30 18:02:04 2020 -0500

       remove unused

      commit fd4f7eb0b935e5a838810564fd549afe710ae19a
      Author: James Bardin <j.bardin@gmail.com>
      Date:   Wed Oct 21 13:06:23 2020 -0400

       remove prefixed io
   
       The main process is now handling what output to print, so it doesn't do
       any good to try and run it through prefixedio, which is only adding
       extra coordination to echo the same data.

      commit 5ac311e2a91e381e2f52234668b49ba670aa0fe5
      Author: Martin Atkins <mart@degeneration.co.uk>
      Date:   Wed May 3 16:25:41 2017 -0700

       main: synchronize writes to VT100-faker on Windows
   
       We use a third-party library "colorable" to translate VT100 color
       sequences into Windows console attribute-setting calls when Terraform is
       running on Windows.
   
       colorable is not concurrency-safe for multiple writes to the same console,
       because it writes to the console one character at a time and so two
       concurrent writers get their characters interleaved, creating unreadable
       garble.
   
       Here we wrap around it a synchronization mechanism to ensure that there
       can be only one Write call outstanding across both stderr and stdout,
       mimicking the usual behavior we expect (when stderr/stdout are a normal
       file handle) of each Write being completed atomically.
      

