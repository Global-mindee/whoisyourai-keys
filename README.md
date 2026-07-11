# whoisyourai-keys — 이용 키 · 킬스위치 서버

이 저장소는 `whoisyourai-*` MCP 팩의 **이용 키 배급**과 **원격 서비스 중단(킬스위치)** 을 담당합니다. 엔진은 시작 시 이 저장소의 `status.json`을 GitHub raw로 1회 조회합니다.

```
https://raw.githubusercontent.com/Global-mindee/whoisyourai-keys/main/status.json
```

## status.json 형식

```json
{
  "schema": 1,
  "service": { "active": true, "message": "" },
  "packs": {
    "marx-manifesto-1848": { "active": true, "key": "<hex 32바이트>" },
    "nietzsche-zarathustra-1883": { "active": true, "key": "<hex>" }
  }
}
```

## 운영

- **특정 책 중단**: 해당 팩의 `"active": false`. 새 대화에서 복호가 차단됩니다(이미 7일 캐시를 받은 설치본은 캐시 만료 후 차단).
- **전체 중단**: `service.active: false` + `message`에 안내 문구.
- **키 교체**: `key` 값 갱신 + 해당 팩을 새 키로 재빌드·재배포.

## 정직한 한계 (숨기지 않음)

이 키는 공개 URL로 배급됩니다. 따라서:

- 제공하는 것: (a) npm·GitHub·검색에 **평문 노출 0** (b) **원격 중단권**(신규 세션·신규 다운로드 차단).
- 제공하지 못하는 것: 이미 키를 받은 이용자, 코드에서 URL을 추출해 직접 키를 가져오는 이용자의 **복호·재배포**. 이는 기술이 아니라 라이선스(법, CC BY-NC-ND 4.0)가 담당합니다.

이것은 DRM이 아니라 **정적 유출 차단 + 원격 차단권** 두 가지만 제공하는 억제 계층입니다.

## 보안

- 이 저장소 자체는 **공개(public)** 여야 합니다(엔진이 raw로 조회). 키가 공개된다는 뜻이며, 위 한계가 그 결과입니다.
- 완전한 통제가 필요한 상용 신간은 이 방식이 아니라 **서버 발췌 API(라이브 브리지)** 로 가야 합니다 — 원문이 단말에 내려가지 않는 별개 트랙.
