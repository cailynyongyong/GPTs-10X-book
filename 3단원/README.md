# PART 03. 다양한 검색 엔진을 GPTs와 연동하기

## SerpAPI 링크

```
https://serpapi.com
```

## 구글 검색 엔진 연동

### 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Search API",
    "description": "API for searching Google using specific queries.",
    "version": "v1.0.0"
  },
  "servers": [
    {
      "url": "https://serpapi.com"
    }
  ],
  "paths": {
    "/search": {
      "get": {
        "summary": "Search Google",
        "operationId": "searchEngine",
        "description": "Retrieves search results from Google for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": ["google"]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google.",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "api_key",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "내 SerpAPI API key 넣어주기"
              ]
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successful response with search results.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "results": {
                      "type": "array",
                      "items": {
                        "type": "object"
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

### 프롬프트

```
너는 시장조사를 대신 해주는 리서치 GPT야. 다음 단계를 통해 시장 조사를 도와줘.
1.시장 조사를 시작하기 전에 먼저 사용자에게 구체적으로 어떤 분야, 어느 나라 시장 조사를 하고 싶은지 물어봐줘.
2. 그다음 사용자의 정보를 토대로 SerpAPI를 호출하여 구글 검색을 통해 사용자가 필요한 시장 조사 정보를 검색해서 요약해줘.
3. 시장 조사 결과를 테이블로 나타내줘. 예를 들어, 만약 사용자가 “생성 AI 스타트업 시장조사해 줘.’라고 하면 스타트업의 이름, 직원 수, 투자 받은 금액, 회사가 제공하고 있는 서비스에 대한 설명 을 테이블로 만들어줘.
```

## 입사 지원서 자동화

### 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Jobs API",
    "description": "API for searching Google Jobs using specific queries.",
    "version": "v1.0.0"
  },
  "servers": [
    {
      "url": "https://serpapi.com"
    }
  ],
  "paths": {
    "/search": {
      "get": {
        "summary": "Search Google Jobs",
        "operationId": "searchJobs",
        "description": "Retrieves search results from Google Jobs for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_jobs'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_jobs"
              ]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google Jobs.",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "hl",
            "in": "query",
            "description": "Query to search for on Google Jobs.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "ko"
              ]
            }
          },
          {
            "name": "api_key",
            "in": "query",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "내 SerpAPI API key"
              ]
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successful response with search results.",
            "content": {
              "application/json": {
                "schema": {
                  "type": "object",
                  "properties": {
                    "results": {
                      "type": "array",
                      "items": {
                        "type": "object"
                      }
                    }
                  }
                }
              }
            }
          }
        }
      }
    }
  }
}
```

### 프롬프트

```
너는 사용자의 이력서 내용을 바탕으로 관련 채용 정보를 찾아주고, 자기소개서까지 작성해주는 GPT야.

1. 사용자가 이력서를 업로드하면 이력서 내용과 관련된 채용 정보를 SerpAPI 액션인 searchJobs를 통해 찾아줘.
2. 찾은 채용 정보를 나열해줘. 정보를 나열할 때에는 Job 이름, 설명, Qualifications(자격 요건), Responsibilities(업무 역할) 내용을 꼭 포함해서 알려줘.
3. 사용자가 그중에서 지원하고 싶은 채용 정보가 있는지 물어봐줘.
4. 선택을 하면 해당 채용 정보와 사용자의 이력서 내용을 바탕으로 자기소개서를 작성해줘. 단계별로 천천히 생각하면서 답변을 해줘.
```
