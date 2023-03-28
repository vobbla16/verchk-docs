---
title: Использование инструмента
---

## Подкоманды
На данный момент инструмент имеет 4 подкоманды

### Подкоманда `show-targets`
Показывает список всех установленных в этой сборке расширений для сканирования сервисов: название сканируемой расширением системы и базовое CPE имя

Пример вывода(в человекоситаемом формате):
```text
All available systems to scan:
╭─┬──────────┬─────────────────────────────────────────────────────╮
│#│Name      │Base CPE name                                        │
├─┼──────────┼─────────────────────────────────────────────────────┤
│0│Confluence│cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
│1│Grafana   │cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*            │
╰─┴──────────┴─────────────────────────────────────────────────────╯
```

### Подкоманда `determine (url)`
Позволяет определить установленную на переданном URL систему. Одновременно запускаются проверки всеми расширениями, статус проверки для каждого расширения покзывается в реальном времени(можно отключить, см. [тихий режим]({{< relref "#опция--s-wip" >}})).

Пример вывода:
```text
✓ Target is Confluence
✗ Target is not Grafana

Possibly installed on endpoint:
╭─┬─────────────┬─────────────────────────────────────────────────────╮
│#│Target system│Base CPE name                                        │
├─┼─────────────┼─────────────────────────────────────────────────────┤
│0│Confluence   │cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
╰─┴─────────────┴─────────────────────────────────────────────────────╯
```

### Подкоманда `determine-version (url)`
Позволяет определить систему и её версию, установленную на переданном URL. Так же, как и в `determine` процесс всех проверок показывается в реальном времени знаками.

Пример вывода:
```text
✓ Target is Confluence
✗ Target is not Grafana

✓ Found Confluence with version 7.13.0
Possible versions of systems possibly installed on endpoint:
╭─┬─────────────┬───────╮
│#│Target system│Version│
├─┼─────────────┼───────┤
│0│Confluence   │7.13.0 │
╰─┴─────────────┴───────╯
```

### Подкоманда `get-cves (url)`
Позволяет определить уязвимости, которым подвержена версия системы, установленная на данном URL.

Пример выводы:
```text
✓ Target is Confluence
✗ Target is not Grafana

✓ Found Confluence with version 7.13.0

✓ Found 3 CVEs for Confluence 7.13.0 from NVD API

Confluence 7.13.0:
╭─┬──────────────┬────────────┬───────────────────┬─────────────────╮
│#│CVE ID        │CVSS version│CVSS score,severity│Publication date │
├─┼──────────────┼────────────┼───────────────────┼─────────────────┤
│0│CVE-2022-26134│CVSS v3.1   │9.8 CRITICAL       │22:15:7 3.6.2022 │
│1│CVE-2022-26136│CVSS v3.1   │9.8 CRITICAL       │18:15:8 20.7.2022│
│2│CVE-2022-26137│CVSS v3.1   │8.8 HIGH           │18:15:8 20.7.2022│
╰─┴──────────────┴────────────┴───────────────────┴─────────────────╯
```

#### Опция `-d`
Позволяет вывести больше информации о каждой уязвимости.

{{< details title="Пример вывода" >}}
```text
✓ Target is Confluence
✗ Target is not Grafana

✓ Found Confluence with version 7.13.0

✓ Found 3 CVEs for Confluence 7.13.0 from NVD API

Confluence 7.13.0:
╭─┬──────────────┬────────────┬───────────────────┬─────────────────╮
│#│CVE ID        │CVSS version│CVSS score,severity│Publication date │
├─┼──────────────┼────────────┼───────────────────┼─────────────────┤
│0│CVE-2022-26134│CVSS v3.1   │9.8 CRITICAL       │22:15:7 3.6.2022 │
│1│CVE-2022-26136│CVSS v3.1   │9.8 CRITICAL       │18:15:8 20.7.2022│
│2│CVE-2022-26137│CVSS v3.1   │8.8 HIGH           │18:15:8 20.7.2022│
╰─┴──────────────┴────────────┴───────────────────┴─────────────────╯

CVE ID: CVE-2022-26134
CVSS version: CVSS v3.1
CVSS base score, severity: 9.8 CRITICAL
CVSS vector string: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
Source: security@atlassian.com
Publication date: 22:15:7 3.6.2022
Vulnerability status: Modified
Description: In affected versions of Confluence Server and Data Center, an OGNL injection vulnerability exists that would allow an unauthenticated attacker to execute arbitrary code on a Confluence Server or Data Center instance. The affected versions are from 1.3.0 before 7.4.17, from 7.13.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and from 7.18.0 before 7.18.1.

CVE ID: CVE-2022-26136
CVSS version: CVSS v3.1
CVSS base score, severity: 9.8 CRITICAL
CVSS vector string: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
Source: security@atlassian.com
Publication date: 18:15:8 20.7.2022
Vulnerability status: Analyzed
Description: A vulnerability in multiple Atlassian products allows a remote, unauthenticated attacker to bypass Servlet Filters used by first and third party apps. The impact depends on which filters are used by each app, and how the filters are used. This vulnerability can result in authentication bypass and cross-site scripting. Atlassian has released updates that fix the root cause of this vulnerability, but has not exhaustively enumerated all potential consequences of this vulnerability. Atlassian Bamboo versions are affected before 8.0.9, from 8.1.0 before 8.1.8, and from 8.2.0 before 8.2.4. Atlassian Bitbucket versions are affected before 7.6.16, from 7.7.0 before 7.17.8, from 7.18.0 before 7.19.5, from 7.20.0 before 7.20.2, from 7.21.0 before 7.21.2, and versions 8.0.0 and 8.1.0. Atlassian Confluence versions are affected before 7.4.17, from 7.5.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and version 7.21.0. Atlassian Crowd versions are affected before 4.3.8, from 4.4.0 before 4.4.2, and version 5.0.0. Atlassian Fisheye and Crucible versions before 4.8.10 are affected. Atlassian Jira versions are affected before 8.13.22, from 8.14.0 before 8.20.10, and from 8.21.0 before 8.22.4. Atlassian Jira Service Management versions are affected before 4.13.22, from 4.14.0 before 4.20.10, and from 4.21.0 before 4.22.4.

CVE ID: CVE-2022-26137
CVSS version: CVSS v3.1
CVSS base score, severity: 8.8 HIGH
CVSS vector string: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H
Source: security@atlassian.com
Publication date: 18:15:8 20.7.2022
Vulnerability status: Analyzed
Description: A vulnerability in multiple Atlassian products allows a remote, unauthenticated attacker to cause additional Servlet Filters to be invoked when the application processes requests or responses. Atlassian has confirmed and fixed the only known security issue associated with this vulnerability: Cross-origin resource sharing (CORS) bypass. Sending a specially crafted HTTP request can invoke the Servlet Filter used to respond to CORS requests, resulting in a CORS bypass. An attacker that can trick a user into requesting a malicious URL can access the vulnerable application with the victim’s permissions. Atlassian Bamboo versions are affected before 8.0.9, from 8.1.0 before 8.1.8, and from 8.2.0 before 8.2.4. Atlassian Bitbucket versions are affected before 7.6.16, from 7.7.0 before 7.17.8, from 7.18.0 before 7.19.5, from 7.20.0 before 7.20.2, from 7.21.0 before 7.21.2, and versions 8.0.0 and 8.1.0. Atlassian Confluence versions are affected before 7.4.17, from 7.5.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and version 7.21.0. Atlassian Crowd versions are affected before 4.3.8, from 4.4.0 before 4.4.2, and version 5.0.0. Atlassian Fisheye and Crucible versions before 4.8.10 are affected. Atlassian Jira versions are affected before 8.13.22, from 8.14.0 before 8.20.10, and from 8.21.0 before 8.22.4. Atlassian Jira Service Management versions are affected before 4.13.22, from 4.14.0 before 4.20.10, and from 4.21.0 before 4.22.4.
```
{{< /details >}}


## Общие опции

### Опция `-o`
Позволяет использовать другие форматы вывода.

Вывод с опцией `-o console`(стандартное значение):
```text
All available systems to scan:
╭─┬──────────┬─────────────────────────────────────────────────────╮
│#│Name      │Base CPE name                                        │
├─┼──────────┼─────────────────────────────────────────────────────┤
│0│Confluence│cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
│1│Grafana   │cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*            │
╰─┴──────────┴─────────────────────────────────────────────────────╯
```

Вывод с опцией `-o csv`:
```text
All available systems to scan:
#,Name,Base CPE name
0,Confluence,cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*
1,Grafana,cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*
```

### Опция `-s` *(WIP)*
Позволяет отключить вывод дополнительных сообщений, полезных для пользователя, но не удобных про машинной обработке вывода. То есть, выводится только сам результат.

Вывод `verchk determine url`:
```text
✓ Target is Confluence
✗ Target is not Grafana

Possibly installed on endpoint:
╭─┬─────────────┬─────────────────────────────────────────────────────╮
│#│Target system│Base CPE name                                        │
├─┼─────────────┼─────────────────────────────────────────────────────┤
│0│Confluence   │cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
╰─┴─────────────┴─────────────────────────────────────────────────────╯
```

Вывод `verchk -s determine url`:
```text
╭─┬─────────────┬─────────────────────────────────────────────────────╮
│#│Target system│Base CPE name                                        │
├─┼─────────────┼─────────────────────────────────────────────────────┤
│0│Confluence   │cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
╰─┴─────────────┴─────────────────────────────────────────────────────╯
```