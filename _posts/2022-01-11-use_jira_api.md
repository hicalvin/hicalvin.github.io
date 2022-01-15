---
layout: post
title:  "玩玩Jira的API"
date:   2022-01-11 21:58:50 +0800
category: tech
---

目前很多敏捷团队基本上都用了Jira来管理sprint，但是总是会有同学忘了去更新自己的user story的状态，所以就尝试了一下用api的方式拿到当前sprint的user story下面的状态，然后根据时间来提醒可能忘了更新状态的开发人员去更新。

用到了requests这个http访问的神器，而且结果都是JSON结果，所以直接操作就行了。之前还尝试过页面抓取，其实也能实现，只不过页面结构当然不能跟JSON相比，所以有了RESTful API当然是更好地选择。

这里略过了OAuth1的部分，直接跳到API

[Jira REST API](https://docs.atlassian.com/software/jira/docs/api/REST/7.6.1/) 提供了Jira相关的API列表，

- 要获得当前活动的sprint，需要通过[Get all boards](https://docs.atlassian.com/jira-software/REST/7.3.1/#agile/1.0/board-getAllBoards)获得相关的board列表，查询参数可以用name来模糊匹配。
- 之后根据获得的boardID，传给 [Get All Sprints](https://jira-eng-gpk2.cisco.com/jira/rest/agile/1.0/board/{{jira_boardid}}/sprint?state=active)，带上参数*state=active* 获得当前active的sprint. 
- 最后通过[Get issues for sprint](https://docs.atlassian.com/jira-software/REST/7.3.1/#agile/1.0/sprint-getIssuesForSprint) 来拿到当前sprint的所有issue。

```python
def get_all_active_sprints():
    token_auth = get_token_auth()
    sprint_list = []
    for board_id in Jira_board_ID:
        active_sprint_url = get_active_sprint.format(board_id)
        response = requests.get(active_sprint_url, auth=token_auth)
        response_json = response.json()
        active_sprint = response_json['values'][0]
        sprint = Sprint(active_sprint['id'], active_sprint['state'], active_sprint['startDate'], active_sprint['endDate'])
        print(sprint)
        sprint_list.append(sprint)
    return sprint_list
 
def get_issue_by_oauth():
    token_auth = get_token_auth()
    
    # Perform request, authenticating with the OAuth authentication helper.
    response = requests.get(search_issue_by_jql, auth=token_auth)
    response_json = response.json()

    issue_list = []
    for issue in response_json['issues']:
        issue_key = issue['key']
        status = issue['fields']['status']['name']
        assignee_name = issue['fields']['assignee']['displayName']
        quick_notes = issue['fields']['customfield_13000']
        issue = Issue(issue_key, status, assignee_name, quick_notes)
        print(issue)
        issue_list.append(issue)

    return issue_list

def get_token_auth():
    # Create OAuth authentication helper.
    token_auth = OAuth1(client_key='OauthKey',
                    resource_owner_key=ACCESS_TOKEN,
                    signature_method=SIGNATURE_RSA,
                    rsa_key=PRIVATE_KEY,
                    signature_type='auth_header')

    return token_auth

def main():
    get_all_active_sprints()

if __name__ == '__main__':
    main()
```


## Reference

1. [https://developer.atlassian.com/server/jira/platform/jira-rest-api-examples/#searching-for-issues-examples](https://developer.atlassian.com/server/jira/platform/jira-rest-api-examples/#searching-for-issues-examples)
2. [https://docs.atlassian.com/software/jira/docs/api/REST/7.6.1/](https://docs.atlassian.com/software/jira/docs/api/REST/7.6.1/)
3. [https://docs.atlassian.com/jira-software/REST/7.3.1/#agile/1.0/issue-getIssue](https://docs.atlassian.com/jira-software/REST/7.3.1/#agile/1.0/issue-getIssue)
