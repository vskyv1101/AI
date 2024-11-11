# AI
```
pip install openai==0.28
```
```
import openai

# OpenAI API 키 설정 (본인의 API 키로 교체)
openai.api_key = 'Your_API_KEY'

# ChatGPT에게 질문하는 함수
def ask_chatgpt(food, meal_time):
    # 시스템 메시지를 한국어로 설정
    system_message = (
        "당신은 영양 정보 제공을 전문으로 하는 도움이 되는 어시스턴트입니다. "
        "사용자가 요청할 때 지정된 음식으로 아침, 점심 또는 저녁 메뉴를 추천해 주세요."
    )

    # 질문을 한국어로 작성
    question = f"{food}를 사용한 {meal_time} 메뉴를 추천해 주세요."

    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=[
            {"role": "system", "content": system_message},
            {"role": "user", "content": question}
        ],
        max_tokens=1000,
        temperature=0.7
    )
    return response.choices[0].message['content'].strip()

# 사용자의 질문을 받고 답변하는 함수
def nutrition_bot():
    print("영양 정보 Q&A 봇에 오신 것을 환영합니다! 특정 음식과 식사 시간(아침, 점심, 저녁)을 입력해 주세요.")

    while True:
        # 음식 이름 입력 받기
        food = input("알고 싶은 음식 이름 (종료하려면 '종료' 입력): ")
        if food.lower() == "종료":
            print("영양 정보 Q&A를 종료합니다.")
            break

        # 식사 시간(아침, 점심, 저녁) 입력 받기
        meal_time = input("해당 음식에 대한 식사 시간 (아침/점심/저녁 중 하나를 입력): ")
        if meal_time not in ["아침", "점심", "저녁"]:
            print("올바른 식사 시간을 입력해 주세요.")
            continue

        # ChatGPT로 질문 전달 및 답변 받기
        answer = ask_chatgpt(food, meal_time)
        print(f"{food}로 만든 {meal_time} 메뉴 추천:", answer)

# 봇 실행
nutrition_bot()
```
