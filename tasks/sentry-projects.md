# Sentry 프로젝트 레지스트리

`sentry-issue.md`가 읽는 "Sentry 프로젝트 slug → 코드 레포" 매핑표.

- Sentry 조직: datauniverse-91
- GitHub 이슈 레포: yujii0/sentry-test
- Slack 알림 채널: #sentry-info (C0CM9T0S5BQ). 채널을 바꾸려면 이 값만 고친다. 비우면 Slack 알림을 보내지 않는다.

## 매핑표

- slug: Sentry 이슈 조회 결과의 `Project` 값과 동일해야 한다.
- 코드 레포: GitHub `owner/repo`. 코드가 없으면 `-`.
- `?`는 아직 매핑 미확정. 확정 전까지 코드 분석 없이 Sentry 데이터만으로 초안을 쓴다.

| Sentry 프로젝트 slug | 코드 레포                         |
| -------------------- | --------------------------------- |
| pj-familycare        | yujii0/pj.familycare.ai           |
| pj-antiscam          | yujii0/pj.antiscam.co.kr          |
| pj-autocall          | yujii0/pj.autocall.ai             |
| pj-mfinder           | yujii0/pj.mfinder.co.kr           |
| partner-couponwallet | yujii0/partner.couponwallet.co.kr |
| partner-familycare   | yujii0/partner.familycare.ai      |
| hp-antiscam          | yujii0/www.antiscam.co.kr         |
| hp-familycare        | yujii0/www.familycare.ai          |
| hp-mfinder           | yujii0/www.mfinder.co.kr          |
| hp-autocall          | yujii0/www.autocall.ai            |
| hp-couponwallet      | ?                                 |
| svc-couponwallet     | yujii0/svc.couponwallet.co.kr     |
