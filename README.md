# AI
```
pip install openai==0.28
```
```
import openai

# OpenAI API 키 설정 (본인의 API 키로 교체)
openai.api_key = 'Your_API_KEY'

# ChatGPT에게 질문하는 함수
def ask_chatgpt(question):
    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",  # 사용할 모델 선택
        messages=[
            {"role": "system", "content": "You are a helpful assistant specializing in nutrition information."},
            {"role": "user", "content": question}
        ],
        max_tokens=3000,  # 응답의 최대 길이
        temperature=0.7  # 응답의 다양성 조절
    )
    return response.choices[0].message['content'].strip()

# 사용자의 질문을 받고 답변하는 함수
def nutrition_bot():
    print("궁금한 영양 정보를 입력하세요.")
    
    while True:
        question = input("질문 (종료하려면 '종료' 입력): ")
        if question.lower() == "종료":
            print("영양 정보 Q&A를 종료합니다.")
            break
        
        # ChatGPT로 질문 전달 및 답변 받기
        answer = ask_chatgpt(question)
        print("답변:", answer)

# 봇 실행
nutrition_bot()
```
