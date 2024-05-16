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

### 예시 이력서

```
이력서

개인 정보
이름: 홍길동
주소: 서울특별시 강남구 역삼동
연락처: 010-1234-5678
이메일: honggildong@example.com
생년월일: 1990년 1월 1일

학력
2020. 3 - 2024. 2 서울대학교, 컴퓨터공학과 학사

경력
2022. 6 - 2023. 8 ABC 기술 회사, 소프트웨어 엔지니어 인턴

기술및능력
- Python, Java, C++ 프로그래밍 언어 능숙
- 웹 개발: HTML, CSS, JavaScript, React
- 데이터베이스 관리: MySQL, MongoDB
-통신능력및팀워크

자격증및인증
2023. 5 정보처리기사
```

## 네이버 뉴스 자동화

### 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Naver API",
    "description": "API for searching Naver using specific queries.",
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
        "summary": "Search Naver",
        "operationId": "searchNaver",
        "description": "Retrieves search results from Naver for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'naver'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "naver"
              ]
            }
          },
          {
            "name": "query",
            "in": "query",
            "description": "Query to search for on Naver.",
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
너는 사용자 대신 네이버 뉴스를 찾아주고 요약해주는 GPT야.
1. 사용자가 검색어를 입력하면 관련 뉴스를 SerpAPI 액션인 searchNaver를 통해 찾아줘.
2.관련 기사를 다섯 가지 불러와줘. 뉴스 기사를 불러올 때 꼭 가장 최신 뉴스만 불러오도록 해줘.
파라미터 값 중에 “news_date”: “1일 전” 기사들만 가져와줘.
3.각 뉴스의 제목, 날짜 및 시간, 간단한 내용 요약과 기사 링크를 꼭 포함해서 알려줘.
```

## 유튜브 추천 영상

### 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Youtube API",
    "description": "API for searching Youtube using specific queries.",
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
        "summary": "Search Youtube",
        "operationId": "searchYoutube",
        "description": "Retrieves search results from Youtube for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'youtube'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "youtube"
              ]
            }
          },
          {
            "name": "search_query",
            "in": "query",
            "description": "Query to search for on Youtube.",
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
너는 사용자가 10X AI Club 유튜브 채널에게 질문을 하면 답변을 해주는 GPT야.
10X AI Club은 생성 AI에 대한 이론과 실습을 주로 다루는 채널이야.
OpenAI, GPT-4, LLM을 활용한 프로젝트들을 프로그래밍에 대해 아무것도 모르더라도 개발이 가능하도록 기초부터 차근 차근 쉽게 설명해주는 채널이야.

1. SerpAPI를 통해 “channel name”이 꼭 “10X AI Club”인 채널의 영상들만 불러오도록 해 줘.
다른 채널 영상들은 불러오지 말아줘.
2.사용자가 생성AI와 관련된 질문을 하면 답변을 해주고, 관련된 내용을 다루고 있는 채널 내의 동영상을 추천해줘.
3. 동영상을 추천해줄때 영상의 제목, 설명, 영상 길이, 조회수도 같이 포함해서 답변해줘.
예를 들어, 사용자가 ‘OpenAI Sora는 무엇인가요?’라고 질문하면 이런 식으로 답변해줘:

답변: OpenAI Sora는....

**10X AI Club 추천 영상**:
📍제목: 이제는 집에서 혼자 영화까지 만들 수 있어요.. | OpenAI Sora
📍설명: OpenAI Sora에 대해 설명하는 영상입니다.
📍영상 길이: 09:38
📍조회수: 10000
```

## 논문 리서치 자동화

### Google Scholar 스키마 기본 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Scholar API",
    "description": "API for searching Google Scholar using specific queries.",
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
        "summary": "Search Google Scholar",
        "operationId": "searchGoogleScholar",
        "description": "Retrieves search results from Google Scholar for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_scholar'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_scholar"
              ]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google Scholar.",
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

### Google Scholar 스키마 추가 옵션 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Scholar API",
    "description": "API for searching Google Scholar using specific queries.",
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
        "summary": "Search Google Scholar",
        "operationId": "searchGoogleScholar",
        "description": "Retrieves search results from Google Scholar for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_scholar'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_scholar"
              ]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google Scholar.",
            "required": true,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "as_ylo",
            "in": "query",
            "description": "Query to search for on Google Scholar.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "2018"
              ]
            }
          },
          {
            "name": "hl",
            "in": "query",
            "description": "Query to search for on Google Scholar.",
            "required": true,
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

### Google Patents 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Patents API",
    "description": "API for searching Google Patents using specific queries.",
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
        "summary": "Search Google Patents",
        "operationId": "searchGooglePatents",
        "description": "Retrieves search results from Google Patents for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_patents'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_patents"
              ]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google Scholar.",
            "required": false,
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

### 두개 검색 엔진 합친 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Research API",
    "description": "API for searching Google Scholar and Patents using specific queries.",
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
        "summary": "Search Google Research",
        "operationId": "searchGoogleResearch",
        "description": "Retrieves search results from Google Scholar and Patents for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_patents' or ‘google_scholar.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_patents", “google_scholar”
              ]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google Scholar or Google Patents.",
            "required": false,
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
너는 사용자 대신 논문과 특허를 찾아주고 요약해주는 GPT야.
1. 사용자가 검색어를 입력하면 관련 논문을 찾고 싶은지, 특허를 찾고 싶은지 물어봐줘.
2. 논문을 찾아달라고 요청하면 SerpAPI 액션에서 engine: google_scholar를 이용하여 검색 해줘.
3. 특허를 찾아달라고 요청하면 SerpAPI 액션에서 engine: google_patents를 이용하여 검색 해줘.
4. 둘다 요청하면 각각의 검색 엔진을 사용해서 찾아줘.
5. 결과물은 3개 정도 요약해서 찾아줘. 모두 한국어로 답변해주고, 논문 혹은 특허의 제목, 저자, 설명, 링크도 함께 포함해줘.

예시 답변:
**[검색어] 관련 논문**:
📍제목:
📍저자:
📍설명:
📍링크:

**[검색어] 관련 특허**:
📍제목:
📍저자:
📍설명:
📍링크:
```

## 여행 일정 자동화

### Google Maps 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Maps API",
    "description": "API for searching Google Maps using specific queries.",
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
        "summary": "Search Google Maps",
        "operationId": "searchGoogleMaps",
        "description": "Retrieves search results from Google Maps for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_maps'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_maps"
              ]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google Maps.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "ll",
            "in": "query",
            "description": "Latitude and longitude for the search, followed by zoom level.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "type",
            "in": "query",
            "description": "Type of the search.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "search"
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

### Directions API 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Directions API",
    "description": "API for searching Google Directions using specific queries.",
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
        "summary": "Search Google Directions",
        "operationId": "searchGoogleDirections",
        "description": "Retrieves search results from Google Maps Directions for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_maps_directions'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_maps_directions"
              ]
            }
          },
          {
            "name": "start_addr",
            "in": "query",
            "description": "Start address",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "end_addr",
            "in": "query",
            "description": "End address",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "distance_unit",
            "in": "query",
            "description": "Type of the search.",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "0"
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

### 두개 검색 엔진 합친 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Google Maps API",
    "description": "API for searching Google Maps and Directions using specific queries.",
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
        "summary": "Search Google Maps",
        "operationId": "searchGoogleMaps",
        "description": "Retrieves search results from Google Maps & Directions for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'google_maps' or 'google_maps_directions'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": [
                "google_maps", "google_maps_directions"
              ]
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google Maps.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "ll",
            "in": "query",
            "description": "Latitude and longitude for the search, followed by zoom level. Use for Google Maps",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "type",
            "in": "query",
            "description": "Type of the search. Use for Google Maps",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "search"
              ]
            }
          },
          {
            "name": "start_addr",
            "in": "query",
            "description": "Start address. Use for Directions",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "end_addr",
            "in": "query",
            "description": "End address. Use for Directions",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "distance_unit",
            "in": "query",
            "description": "Type of the search. Use for Directions",
            "required": false,
            "schema": {
              "type": "string",
              "enum": [
                "0"
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
당신은 사용자의 개인 취향에 맞게 여행지 추천, 맛집 추천, 일정표 계획을 짜주는 GPT입니다.
검색을 하기 전에 사용자에게 몇 가지 질문을 합니다. 질문을 한꺼번에 하지 말고 꼭 한번에 한개씩 해주세요:

1. 여행하고자 하는 장소는 어디입니까?
[주관식 답변]

2. 여행 예산은 어느 정도인가요?
   A. 경제적 (저렴한)
   B. 보통
   C. 고급 (비싼)
   D. 무제한

3. 여행 스타일을 선택해주세요.
   A. 박물관 및 관광
   B. 음식 투어
   C. 자연 탐방
   D. 모험 및 액티비티

4. 선호하는 음식 유형은 무엇입니까?
   A. 현지 전통 음식
   B. 인터내셔널 요리
   C. 건강식
   D. 길거리 음식

5. 여행 중 중요하게 생각하는 것은 무엇입니까?
   A. 문화 체험
   B. 휴식 및 리프레시
   C. 쇼핑 및 엔터테인먼트
   D. 교육적 경험

질문이 끝나면 이제 사용자의 개인 취향 정보를 바탕으로 검색을 실행해주세요.
SerpAPI 액션을 통해 연동한 "searchGoogleMaps" function의 Google Maps API로 1) 관광지(Things to do), 2) 맛집(Restaurants) 추천을 해주세요.
검색을 할때, 사용자가 알려준 위치 정보를 위도와 경도로 변환해서 "ll" 파라미터에 저장한 다음 검색해주세요.
ll 파라미터 형식은 다음과 같습니다: @ + latitude + , + longitude + , + zoom
예시: @40.7455096,-74.0083012,14z

답변할때 세개씩 추천해주세요.

##예시 답변
**주요 관광지**
- 관광 명소 이름
- 평점
- 설명
- 관련 링크

**맛집 추천**
- 식당 이름
- 평점
- 식당 설명
- 대표 추천 메뉴
- 가격
- 가격대 및 설명
- 관련 링크

추천해준 후, 사용자에게 마음에 드는 곳들을 선택하라고 물어봐주세요.

사용자가 마음에 드는 곳을 선택했다면 다음 질문을 물어봐주세요:
“이제 여행 일정표를 만들어 드리겠습니다. 그 전에, 여행 기간은 몇일이며, 숙소 위치는 어디인가요?”

일정표를 만들때에는 SerpAPI의 "searchGoogleMaps" function에서 google_maps_directions 엔진을 사용해서 검색해주세요.
Don't use google_maps engine.
사용자에게 받은 정보를 바탕으로 여행 일정표를 만들어주세요. 꼭 표로 시각화해주세요.

##표를 만들때 고려해야 할 사항:
- 천천히 단계별로 생각하면서 계산해줘
- 사용자의 취향과 관심사가 반영돼야 함
- 숙소(start_addr)와 관광지 혹은 맛집(end_addr) 거리가 멀지 않아야 함
- 숙소에서부터 출발해서 각 관광지/맛집에서 소요하는 시간 예측해서 시간표 작성
- 각 관광지/맛집 사이의 거리와 소요 시간을 계산해서 최적의 best optimal route를 계산해야 함

##표에 들어갈 정보:
- 관광지 혹은 맛집 이름, 설명, 가격대
- 위치
- 숙소 혹은 이전 관광지/맛집에서부터의 거리 및 소요되는 시간
- 시간표
```

## 여러 검색 엔진 연동하기

### 스키마 코드

```
{
  "openapi": "3.1.0",
  "info": {
    "title": "Multiple Search API",
    "description": "API for searching Google, Youtube, Naver using specific queries.",
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
        "summary": "Search Naver, Google, or Youtube",
        "operationId": "searchEngine",
        "description": "Retrieves search results from Naver, Google, or Youtube for a given query.",
        "parameters": [
          {
            "name": "engine",
            "in": "query",
            "description": "Search engine to use, set to 'naver' or 'google' or 'youtube'.",
            "required": true,
            "schema": {
              "type": "string",
              "enum": ["google", "naver", "youtube"],
            }
          },
          {
            "name": "q",
            "in": "query",
            "description": "Query to search for on Google.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "query",
            "in": "query",
            "description": "Query to search for on Naver.",
            "required": false,
            "schema": {
              "type": "string"
            }
          },
          {
            "name": "search_query",
            "in": "query",
            "description": "Query to search for on Youtube.",
            "required": false,
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
