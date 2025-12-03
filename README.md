# 注册
POST调用 http://localhost:3000/api/v1/signup
```json
{
  "voter": {
    "phone": "23456789",
    "name": "Alice",
    "password": "secret123",
    "password_confirmation": "secret123"
  }
}
```
返回
```json
{
    "voter": {
        "id": 2,
        "phone": "23456789",
        "name": "Alice",
        "phone_verified": false,
        "created_at": "2025-12-03T03:12:17Z"
    }
}
```
# 发验证码
POST http://localhost:3000/api/v1/signup/send_code
```json ```

返回

从服务器日志中看到 验证码信息

# 验证

POST http://localhost:3000/api/v1/signup/verify

请求体
```json
{
  "voter": {
    "phone": "23456789",
    "verification_code": "376993"
  }
}
```

返回
```json
{
    "voter": {
        "id": 2,
        "phone": "23456789",
        "name": "Alice",
        "phone_verified": true,
        "created_at": "2025-12-03T03:12:17Z"
    }
}
```
# 登录

POST  http://localhost:3000/api/v1/login

请求体
```json
{
  "phone": "23456789",
  "password": "secret123"
}
```
返回
```json
{
    "session": {
        "access_token": "96519936ed31c26947dd623f056d965a0bb58245a860d329c290153ec9160c0b",
        "expires_at": "2025-12-10T03:19:18Z"
    },
    "voter": {
        "id": 2,
        "phone": "23456789",
        "name": "Alice",
        "phone_verified": true
    }
}
```
# 增加候选人 
POST  http://localhost:3000/api/v1/candidates
在请求中headers加入 Authorization  Bearer {access_token}
请求体
```json
{
    "candidate": {
        "name": "Candidate A",
        "description": "测试候选人 A",
        "photo_url": "https://example.com/a.jpg",
        "is_active": true
    }
}
```
返回
```json
{
    "candidate": {
        "id": 1,
        "name": "Candidate A",
        "description": "测试候选人 A",
        "photo_url": "https://example.com/a.jpg",
        "votes_count": 0,
        "has_voted": false
    }
}
```
请求
```json
{
        "candidate": {
          "name": "Candidate B",
          "description": "模特与舞者，擅长公众演讲，致力于女性权益倡导。",
          "photo_url": "https://example.com/photos/b.jpg",
          "is_active": true
        }
}
```
返回
```json
{
    "candidate": {
        "id": 2,
        "name": "Candidate B",
        "description": "模特与舞者，擅长公众演讲，致力于女性权益倡导。",
        "photo_url": "https://example.com/photos/b.jpg",
        "votes_count": 0,
        "has_voted": false
    }
}
```
<h1>查看候选人list</h1>
GET http://localhost:3000/api/v1/candidates

在请求中headers加入 Authorization  Bearer {access_token}

```json
{
    "meta": {
        "page": 1,
        "per_page": 20,
        "total_pages": 1,
        "total_count": 2
    },
    "candidates": [
        {
            "id": 1,
            "name": "Candidate A",
            "description": "测试候选人 A",
            "photo_url": "https://example.com/a.jpg",
            "votes_count": 0,
            "has_voted": false
        },
        {
            "id": 2,
            "name": "Candidate B",
            "description": "模特与舞者，擅长公众演讲，致力于女性权益倡导。",
            "photo_url": "https://example.com/photos/b.jpg",
            "votes_count": 0,
            "has_voted": false
        }
    ]
}
```
# 查看单个候选人
GET http://localhost:3000/api/v1/candidates/2
在请求中headers加入 Authorization  Bearer {access_token}

返回
```json
{
    "candidate": {
        "id": 2,
        "name": "Candidate B",
        "description": "模特与舞者，擅长公众演讲，致力于女性权益倡导。",
        "photo_url": "https://example.com/photos/b.jpg",
        "votes_count": 0,
        "has_voted": false
    }
}
```


# 为候选人投票

POST http://localhost:3000/api/v1/candidates/1/votes
在请求中headers加入 Authorization  Bearer {access_token}
请求体
```json
{}
```
返回
```json
{
    "vote": {
        "id": 1,
        "candidate_id": 1,
        "voter_id": 1,
        "created_at": "2025-12-03T02:39:34Z"
    },
    "candidate": {
        "id": 1,
        "votes_count": 1,
        "has_voted": true
    }
}
```

