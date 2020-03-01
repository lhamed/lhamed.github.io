---
layout: post
title: 재택 근무와 알고리즘 문제 풀다
description: lazy Sat.
modifed: 2020-2-1
tags: [Journal]
---

신종 코로나 바이러스가 아직 기성을 부리고 있다.

우리 회사가 감염자가 돌아다닌 곳과 잘 겹치는 곳이어서 , 이번 주는 재택 근무를 하기로 했다. 

집에서 일하는 건 참 사람을 피곤하게 한다.

아마도 쉬는 공간과 그렇지 않은 공간이 없어서겠지.

월요일 부터 계속 집에 있었더니 좀 울적해졌다. 

이런 저런 생각을 하다가, 퇴근하고 ( 퇴근이래 봤자 잠시 일어났다가 앉는 것에 가깝지만 )

코딩 테스트를 풀어봤다.

전에도 제대로 못 풀었던 백준 알고리즘 문제 1002 번 터렛 문제이다.

지난번에 접근할 때에도, 수학적으로는 거의 맞게 접근했으나 아마 경우의 수 몇개를 빼트렸을 것이다.

지난번엔 c# 이었고 ,  이번에는 c++ 로 풀었다. 

이번에는 훨씬 체계적으로 접근했고 코딩도 깔끔하게 했다고 생각했는데, 

아무리 던져도 오답이었다. 

ㅠㅠ. 

하지만 오늘이 늦었고, 건강이 당연히 먼저니까 우선은 잠에 들기로 했다.

부끄럽지만, 오답 코드를 첨부한다. 

오늘의 부끄러움이 성장의 원동력이 되면 좋겠다. 

오늘 하루를 마무리 한다.

그래도 무기력이 좀 사라진 것 같아 기쁘다. 


```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <cmath>

using namespace std;

double calculate_sum(int a, int b)
{
    double result = (a + b) ;
    return result;
}

double calculate_distance(int x_1, int y_1, int x_2, int y_2)
{

    double diff_x = x_1 - x_2;
    double diff_y = y_1 - y_2;
    double result = diff_x * diff_x + diff_y * diff_y;

    return sqrt (result);
}

int main()
{
    string str_input_raw;

    getline(cin, str_input_raw);

    int repeat_count = stoi(str_input_raw);

    string input_string_array[repeat_count];

    for (int i = 0; i < repeat_count; i++)
    {
        getline(cin, input_string_array[i]);
    }

    for (int i = 0; i < repeat_count; i++)
    {
        str_input_raw = input_string_array[i];

        stringstream ss(str_input_raw);

        string str_temp;

        int input_array[6];

        int index = 0;

        // 2020-1-26 Lhamed : 0 으로 할당하지 않으면 계산 결과가 이상해진다 ?? 아직 원인 모른다.
        while (ss >> str_temp)
        {
            // 2020-1-26 Lhamed : 공백도 숫자로 변환되어서 더해져 버린다.
            if (str_temp != " ")
            {
                input_array[index] = stoi(str_temp);
            }
            index++;
        }

        int x_1 = input_array[0];
        int y_1 = input_array[1];
        int r_1 = input_array[2];
        int x_2 = input_array[3];
        int y_2 = input_array[4];
        int r_2 = input_array[5];

        // infinte point
        if (x_1 == x_2 && y_1 == y_2)
        {
            if (r_1 == r_2)
            {
                cout << -1;
                continue;
            }
            else
            {
                cout << 0;
                continue;
            }
        }

        double sum_radian = calculate_sum(r_1, r_2);
        double distance= calculate_distance(x_1, y_1, x_2, y_2);


        double r_1_square =  r_1 * r_1;
        double r_2_square =  r_2 * r_2;


        if (sum_radian > distance)
        {
            if (2 * r_1_square == distance && 2 * r_2_square != distance)
            {
                if(2 * r_1 < r_2)
                {
                    cout << 0;
                    continue;
                }
            }
            if (2 * r_1_square != distance && 2 * r_2_square == distance )
            {
                if( 2 * r_2 < r_1)
                {
                    cout << 0;
                    continue;
                }
            }
            cout << 2;
            continue;
        }
        else if (sum_radian < distance)
        {
            cout << 0;
            continue;
        }
        else
        {
            cout << 1;
            continue;
        }
    }
}


```
