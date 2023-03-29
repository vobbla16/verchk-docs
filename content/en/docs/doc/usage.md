---
title: Using the tool
---

## Subcommands
At the moment the tool has 4 subcommands

### `show-targets` subcommand
Shows a list of all extensions installed in this assembly for scanning services: the name of the system scanned by the extension and the base CPE name

Sample output (in human readable format):
```text
All available systems to scan:
╭─┬──────────┬─────────────────────────────────────────────────────╮
│#│Name      │Base CPE name                                        │
├─┼──────────┼─────────────────────────────────────────────────────┤
│0│Confluence│cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
│1│Grafana   │cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*            │
╰─┴──────────┴─────────────────────────────────────────────────────╯
```

### `determine (url)` subcommand
Allows you to determine the system installed on the given URL. Checks are run by all extensions at the same time, the check status for each extension is shown in real time (can be disabled, see [quiet mode]({{< relref "#-s-option-wip" >}})).

Sample output:
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

### `determine-version (url)` subcommand
Allows you to determine the system and its version installed on the passed URL. Just like in `determine`, the process of all checks is shown in real time with signs.

Sample output:
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

### `get-cves (url)` subcommand
Allows you to determine the vulnerabilities that affect the version of the system installed at this URL.

Example conclusions:
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

#### `-d` option
Allows you to display more information about each vulnerability.

{{< details title="Sample Output" >}}
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
Description: In versions affected of Confluence Server and Data Center, an OGNL injection vulnerability exists that would allow an unauthenticated attacker to execute arbitrary code on a Confluence Server or Data Center instance. The affected versions are from 1.3.0 before 7.4.17, from 7.13.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and from 7.18.0 before 7.18.1.

CVE ID: CVE-2022-26136
CVSS version: CVSS v3.1
CVSS base score, severity: 9.8 CRITICAL
CVSS vector string: CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H
Source: security@atlassian.com
Publication date: 18:15:8 20.7.2022
Vulnerability status: Analyzed
Description: A vulnerability in multiple Atlassian products allows a remote, unauthenticated attacker to bypass Servlet Filters used by first and third party apps. The impact on which filters are used by each app, and how the filters are used. This vulnerability can result in authentication bypass and cross-site scripting. Atlassian has released updates that fix the root cause of this vulnerability, but has not exhaustively enumerated all potential consequences of this vulnerability. Atlassian Bamboo versions are affected before 8.0.9, from 8.1.0 before 8.1.8, and from 8.2.0 before 8.2.4. Atlassian Bitbucket versions are affected before 7.6.16, from 7.7.0 before 7.17.8, from 7.18.0 before 7.19.5, from 7.20.0 before 7.20.2, from 7.21.0 before 7.21.2, and versions 8.0. 0 and 8.1.0. Atlassian Confluence versions are affected before 7.4.17, from 7.5.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and version 7.21.0. Atlassian Crowd versions are affected before 4.3.8, from 4.4.0 before 4.4.2, and version 5.0.0. Atlassian Fisheye and Crucible versions before 4.8.10 are affected. Atlassian Jira versions are affected before 8.13.22, from 8.14.0 before 8.20.10, and from 8.21.0 before 8.22.4. Atlassian Jira Service Management versions are affected before 4.13.22, from 4.14.0 before 4.20.10, and from 4.21.0 before 4.22.4.

CVE ID: CVE-2022-26137
CVSS version: CVSS v3.1
CVSS base score, severity: 8.8 HIGH
CVSS vector string: CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H
Source: security@atlassian.com
Publication date: 18:15:8 20.7.2022
Vulnerability status: Analyzed
Description: A vulnerability in multiple Atlassian products allows a remote, unauthenticated attacker to cause additional Servlet Filters to be invoked when the application processes requests or responses. Atlassian has confirmed and fixed the only known security issue associated with this vulnerability: Cross-origin resource sharing (CORS) bypass. Sending a specially crafted HTTP request can invoke the Servlet Filter used to respond to CORS requests, resulting in a CORS bypass. An attacker that can trick a user into requesting a malicious URL can access the vulnerable application with the victim’s permissions. Atlassian Bamboo versions are affected before 8.0.9, from 8.1.0 before 8.1.8, and from 8.2.0 before 8.2.4. Atlassian Bitbucket versions are affected before 7.6.16, from 7.7.0 before 7.17.8, from 7.18.0 before 7.19.5, from 7.20.0 before 7.20.2, from 7.21.0 before 7.21.2, and versions 8.0. 0 and 8.1.0. Atlassian Confluence versions are affected before 7.4.17, from 7.5.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and version 7.21.0. Atlassian Crowd versions are affected before 4.3.8, from 4.4.0 before 4.4.2, and version 5.0.0. Atlassian Fisheye and Crucible versions before 4.8.10 are affected. Atlassian Jira versions are affected before 8.13.22, from 8.14.0 before 8.20.10, and from 8.21.0 before 8.22.4. Atlassian Jira Service Management versions are affected before 4.13.22, from 4.14.0 before 4.20.10, and from 4.21.0 before 4.22.4.
```
{{</details>}}


## General Options

### `-o` option
Allows you to use other output formats.

Output with `-o console` (default) option:
```text
All available systems to scan:
╭─┬──────────┬─────────────────────────────────────────────────────╮
│#│Name      │Base CPE name                                        │
├─┼──────────┼─────────────────────────────────────────────────────┤
│0│Confluence│cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
│1│Grafana   │cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*            │
╰─┴──────────┴─────────────────────────────────────────────────────╯
```

Output with `-o csv` option:
```text
All available systems to scan:
#,Name,Base CPE name
0,Confluence,cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*
1,Grafana,cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*
```

### `-s` option *(WIP)*
Allows you to disable the output of additional messages that are useful to the user, but not convenient for machine output processing. That is, only the result is displayed.

Output of `verchk determine url`:
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
