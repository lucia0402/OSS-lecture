#!/bin/bash

PHONEBOOK_FILE="phonebook.txt"
TEMP_FILE="temp_phonebook.txt"


if [ "$#" -ne 2 ]; then
    echo "입력값 오류"
    exit 1
fi

NAME="$1"
PHONE_NUMBER="$2"


if ! [[ "$PHONE_NUMBER" =~ ^[0-9]+$ ]]; then
    echo "입력값 오류 : 전화번호는 숫자만 입력 가능합니다."
    exit 1
fi


if [ ${#PHONE_NUMBER} -eq 10 ]; then
    FORMATTED_PHONE_NUMBER="010-${PHONE_NUMBER:0:4}-${PHONE_NUMBER:4:4}"
elif [ ${#PHONE_NUMBER} -eq 11 ]; then
    FORMATTED_PHONE_NUMBER="${PHONE_NUMBER:0:3}-${PHONE_NUMBER:3:4}-${PHONE_NUMBER:7:4}"
else
    echo "입력값 오류 : 전화번호는 10자리 또는 11자리여야 합니다."
    exit 1
fi


AREA_CODE="${FORMATTED_PHONE_NUMBER%%-*}"
case "$AREA_CODE" in
    "02")
        AREA="서울"
        ;;
    "031")
        AREA="경기"
        ;;
    "032")
        AREA="인천"
        ;;
    "051")
        AREA="부산"
        ;;
    "055")
        AREA="거제"
        ;;
    "010")
        AREA="개인 번호"
        ;;
    *)
        AREA="알 수 없는 지역 번호"
        ;;
esac


if [ ! -f "$PHONEBOOK_FILE" ];then
    touch "$PHONEBOOK_FILE"
fi


if grep -q "^$NAME " "$PHONEBOOK_FILE"; then

    if ! grep -q "^$NAME $FORMATTED_PHONE_NUMBER " "$PHONEBOOK_FILE"; then
        echo "$NAME $FORMATTED_PHONE_NUMBER $AREA" >> "$PHONEBOOK_FILE"
        echo "$NAME $FORMATTED_PHONE_NUMBER $AREA의 정보가 phonebook.txt에 추가 되었습니다."
        exit 0

    else
        echo "$NAME $FORMATTED_PHONE_NUMBER $AREA의 정보가 이미 phonebook.txt에 저장되어 있습니다."
        exit 1
    fi

else

    echo "$NAME $FORMATTED_PHONE_NUMBER $AREA" >> "$PHONEBOOK_FILE"
    echo "$NAME $FORMATTED_PHONE_NUMBER $AREA의 정보가 phonebook.txt에 추가 되었습니다."

    LC_COLLATE=ko_KR.UTF-8 sort -k1,1 "$PHONEBOOK_FILE" > "$TEMP_FILE"
    mv "$TEMP_FILE" "$PHONEBOOK_FILE"

    exit 0
fi


