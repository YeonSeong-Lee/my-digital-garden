---
{"title":"Time Zone","tags":"troubleshooting, timezone, programming","dg-publish":true,"permalink":"/troubleshooting/node-schedule-time-zone/","dgPassFrontmatter":true}
---


# PROBELM

기존에는 `node-schedule`라이브러리에서 timezone설정없이 그대로 코드가 돌아가고 있었다. 
`node-schedule`를 timezone 설정없이 사용하게 되면 서버시간 기준으로 timezone이 돌아간다. 

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
```