

## User check

### 활용
해당 userId가 존재하는지 하지 않는지에 대하여 확인하는 API입니다.

### 샘플 요청
```
http://127.0.0.1:8080/cbank/api/v1/user/test12
```

### 응답 (존재할 경우)
```
{
    "resultCode": "200",
    "resultMsg": "",
    "now": "Mon Dec 06 21:27:10 KST 2021"
}
```

### 응답 (존재하지 않을 경우)
```
{
    "resultCode": "404",
    "resultMsg": "[test12] is not exist User!",
    "now": "Mon Dec 06 21:27:20 KST 2021"
}
```

> #### ⚠ 응답항목  
> resultCode는 200일 경우는 정상이며 그 이외의 값일 경우는 모두 실패입니다.<br>
> resultMsg는 필요할 경우 내용을 적습니다. 특히 실패일 경우 해당 내용을 기록하고 있으니 참고하시기 바랍니다.<br>
> now는 요청온 시간을 기록합니다.

<br>

☕ [전체 API 문서로 돌아가기](/api.md)
