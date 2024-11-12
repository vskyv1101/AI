# AI
```
pip install openai==0.28
```
```
import openai

# OpenAI API 키 설정 (본인의 API 키로 교체)
openai.api_key = 'Your_API_KEY'
# ChatGPT에게 음식 정보를 요청하는 함수
def ask_food_info(food):
    system_message = (
        "당신은 영양 정보 제공을 전문으로 하는 도움이 되는 어시스턴트입니다. "
        "사용자가 특정 음식에 대해 질문하면 해당 음식의 영양 정보와 건강 효능을 설명해 주세요."
    )
    question = f"{food}의 영양 정보와 건강에 좋은 점을 알려주세요."

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

# ChatGPT에게 식사 시간에 따른 메뉴를 요청하는 함수
def ask_menu_suggestion(food, meal_time):
    system_message = (
        "당신은 영양 정보 제공을 전문으로 하는 도움이 되는 어시스턴트입니다. "
        "사용자가 요청할 때 지정된 음식으로 아침, 점심 또는 저녁 메뉴를 추천해 주세요."
    )
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
    print("영양 정보 Q&A 봇에 오신 것을 환영합니다! 먼저 알고 싶은 음식을 입력해 주세요.")

    while True:
        # 첫 번째 단계: 음식 이름 입력 받기
        food = input("알고 싶은 음식 이름 (종료하려면 '종료' 입력): ")
        if food.lower() == "종료":
            print("영양 정보 Q&A를 종료합니다.")
            break

        # 음식에 대한 기본 정보 제공
        food_info = ask_food_info(food)
        print(f"{food}에 대한 정보:", food_info)

        # 두 번째 단계: 식사 시간(아침, 점심, 저녁) 입력 받기
        while True:
            meal_time = input("해당 음식에 대한 식사 시간 (아침/점심/저녁 중 하나를 입력): ")
            if meal_time not in ["아침", "점심", "저녁"]:
                print("올바른 식사 시간을 입력해 주세요.")
                continue

            # 식사 시간에 맞는 메뉴 추천
            menu_suggestion = ask_menu_suggestion(food, meal_time)
            print(f"{food}로 만든 {meal_time} 메뉴 추천:", menu_suggestion)
            break

# 봇 실행
nutrition_bot()

```
