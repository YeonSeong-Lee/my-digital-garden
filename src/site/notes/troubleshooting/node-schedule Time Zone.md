---
{"title":"Time Zone","tags":"troubleshooting, timezone, programming","dg-publish":true,"permalink":"/troubleshooting/node-schedule-time-zone/","dgPassFrontmatter":true}
---


# PROBELM

## problem
연체자에게 슬랙 알람이 우리가 생각한 시간이 아닌 다른 시간에 감

## reason
기존에는 `node-schedule`라이브러리에서 timezone설정없이 그대로 코드가 돌아가고 있었다. 

`node-schedule`를 timezone 설정없이 사용하게 되면  UTC 기준으로 timezone이 돌아간다. 

## 조기에 발견하지 못 한 이유
(기존 로컬에서 개발할 때는 당연히 한국시간이기때문에 확인하지 못했었다.)

# SOULTION

아래와 같이  `rule.tz = 'Asia/Seoul';`을 추가해줘서 해결했다.


```javascript
import * as schedule from 'node-schedule';
 ...

const midnightScheduler = () => {
  const rule = new schedule.RecurrenceRule();
  rule.dayOfWeek = [0, new schedule.Range(0, 6)];
  rule.hour = 0;
  rule.minute = 42;
  rule.tz = 'Asia/Seoul';
  schedule.scheduleJob(rule, async () => {
    await slack.updateSlackId();
    await notifications.notifyReservationOverdue();
  });
};

...

export const scheduler = () => {
  midnightScheduler();
  morningScheduler();
};

export default scheduler;
```


### 관련 PR
https://github.com/jiphyeonjeon-42/backend/pull/260