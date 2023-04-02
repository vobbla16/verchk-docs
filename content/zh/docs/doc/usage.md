---
title: 使用该工具
---

## 子命令
目前，该工具有4个子命令

### `show-targets`子命令
显示在这个组件中安装的所有用于扫描服务的扩展的列表：扩展所扫描的系统名称和基本CPE名称

输出样本（以人可读的格式）：
```text
All available systems to scan:
╭─┬──────────┬─────────────────────────────────────────────────────╮
│#│Name      │Base CPE name                                        │
├─┼──────────┼─────────────────────────────────────────────────────┤
│0│Confluence│cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
│1│Grafana   │cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*            │
╰─┴──────────┴─────────────────────────────────────────────────────╯
```

### `determine (url)`子命令
允许你确定安装在给定URL上的系统。检查由所有扩展同时进行，每个扩展的检查状态都会实时显示（可以禁用，见[quiet mode]({{< relref "#-s-option-wip" >}})）。

输出样本：
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

### `determine-version (url)`子命令
允许你确定系统和它安装在传递的URL上的版本。就像在`determine`中一样，所有检查的过程都会用标志实时显示。

输出样本：
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

### `get-cves (url)`子命令
允许你确定影响安装在这个URL的系统版本的漏洞。

结论示例：
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

#### `-d`选项
允许你显示关于每个漏洞的更多信息。

{{< details title="输出示例">}}}的详细信息。
```text
✓ Target is Confluence
✗ Target is not Grafana

✓ Found Confluence with version 7.13.0

✓ Found 3 CVEs for Confluence 7.13.0 from NVD API

Confluence 7.13.0:
╭─┬──────────────┬────────────┬────────────┬────────────────────────────────────────────┬──────────────────────┬─────────────────┬────────────────────┬─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│#│CVE ID        │CVSS version│CVSS score  │CVSS vector string                          │Source                │Published        │Vulnerability status│Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          │
├─┼──────────────┼────────────┼────────────┼────────────────────────────────────────────┼──────────────────────┼─────────────────┼────────────────────┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│0│CVE-2022-26134│CVSS v3.1   │9.8 CRITICAL│CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H│security@atlassian.com│22:15:7 3.6.2022 │Modified            │In affected versions of Confluence Server and Data Center, an OGNL injection vulnerability exists that would allow an unauthenticated attacker to execute arbitrary code on a Confluence Server or Data Center instance. The affected versions are from 1.3.0 before 7.4.17, from 7.13.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and from 7.18.0 before 7.18.1.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   │
│1│CVE-2022-26136│CVSS v3.1   │9.8 CRITICAL│CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H│security@atlassian.com│18:15:8 20.7.2022│Analyzed            │A vulnerability in multiple Atlassian products allows a remote, unauthenticated attacker to bypass Servlet Filters used by first and third party apps. The impact depends on which filters are used by each app, and how the filters are used. This vulnerability can result in authentication bypass and cross-site scripting. Atlassian has released updates that fix the root cause of this vulnerability, but has not exhaustively enumerated all potential consequences of this vulnerability. Atlassian Bamboo versions are affected before 8.0.9, from 8.1.0 before 8.1.8, and from 8.2.0 before 8.2.4. Atlassian Bitbucket versions are affected before 7.6.16, from 7.7.0 before 7.17.8, from 7.18.0 before 7.19.5, from 7.20.0 before 7.20.2, from 7.21.0 before 7.21.2, and versions 8.0.0 and 8.1.0. Atlassian Confluence versions are affected before 7.4.17, from 7.5.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and version 7.21.0. Atlassian Crowd versions are affected before 4.3.8, from 4.4.0 before 4.4.2, and version 5.0.0. Atlassian Fisheye and Crucible versions before 4.8.10 are affected. Atlassian Jira versions are affected before 8.13.22, from 8.14.0 before 8.20.10, and from 8.21.0 before 8.22.4. Atlassian Jira Service Management versions are affected before 4.13.22, from 4.14.0 before 4.20.10, and from 4.21.0 before 4.22.4.                                                                                                                          │
│2│CVE-2022-26137│CVSS v3.1   │8.8 HIGH    │CVSS:3.1/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H│security@atlassian.com│18:15:8 20.7.2022│Analyzed            │A vulnerability in multiple Atlassian products allows a remote, unauthenticated attacker to cause additional Servlet Filters to be invoked when the application processes requests or responses. Atlassian has confirmed and fixed the only known security issue associated with this vulnerability: Cross-origin resource sharing (CORS) bypass. Sending a specially crafted HTTP request can invoke the Servlet Filter used to respond to CORS requests, resulting in a CORS bypass. An attacker that can trick a user into requesting a malicious URL can access the vulnerable application with the victim’s permissions. Atlassian Bamboo versions are affected before 8.0.9, from 8.1.0 before 8.1.8, and from 8.2.0 before 8.2.4. Atlassian Bitbucket versions are affected before 7.6.16, from 7.7.0 before 7.17.8, from 7.18.0 before 7.19.5, from 7.20.0 before 7.20.2, from 7.21.0 before 7.21.2, and versions 8.0.0 and 8.1.0. Atlassian Confluence versions are affected before 7.4.17, from 7.5.0 before 7.13.7, from 7.14.0 before 7.14.3, from 7.15.0 before 7.15.2, from 7.16.0 before 7.16.4, from 7.17.0 before 7.17.4, and version 7.21.0. Atlassian Crowd versions are affected before 4.3.8, from 4.4.0 before 4.4.2, and version 5.0.0. Atlassian Fisheye and Crucible versions before 4.8.10 are affected. Atlassian Jira versions are affected before 8.13.22, from 8.14.0 before 8.20.10, and from 8.21.0 before 8.22.4. Atlassian Jira Service Management versions are affected before 4.13.22, from 4.14.0 before 4.20.10, and from 4.21.0 before 4.22.4.│
╰─┴──────────────┴────────────┴────────────┴────────────────────────────────────────────┴──────────────────────┴─────────────────┴────────────────────┴─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```
{{</details>}}


## 一般选项

### `-o`选项
允许你使用其他输出格式。

使用`-o console`（默认）选项进行输出：
```text
All available systems to scan:
╭─┬──────────┬─────────────────────────────────────────────────────╮
│#│Name      │Base CPE name                                        │
├─┼──────────┼─────────────────────────────────────────────────────┤
│0│Confluence│cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
│1│Grafana   │cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*            │
╰─┴──────────┴─────────────────────────────────────────────────────╯
```

用`-o csv`选项输出：
```text
All available systems to scan:
#,Name,Base CPE name
0,Confluence,cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*
1,Grafana,cpe:2.3:a:grafana:grafana:*:*:*:*:*:*:*:*
```

### `-s`选项
允许你禁止输出对用户有用，但不便于机器输出处理的额外信息。也就是说，只显示结果。

`verchk determine url`的输出：
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

输出`verchk -s determine url`：
```text
╭─┬─────────────┬─────────────────────────────────────────────────────╮
│#│Target system│Base CPE name                                        │
├─┼─────────────┼─────────────────────────────────────────────────────┤
│0│Confluence   │cpe:2.3:a:atlassian:confluence_server:-:*:*:*:*:*:*:*│
╰─┴─────────────┴─────────────────────────────────────────────────────╯
```
