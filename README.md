# 목차  
1. [기능 설명 및 배운 점](#1.-기능-설명-및-배운-점)
2. [완성 모습](#2.-완성-모습)
3. [벨로그](#3.-벨로그에서-보기)

# 1. 기능 설명 및 배운 점
![](https://velog.velcdn.com/images/kuronuma_daisy/post/b5067d34-9dea-4c0c-b60a-f403e74819ef/image.png)  
`인생 고고` 버튼을 누르면 주사위 두 개가 랜덤으로 굴려진다. 같은 눈의 주사위가 나오면 `잭팟!`이라는 토스트 메시지가 뜬다.


## dataBinding 데이터 바인딩
데이터 바인딩을 사용하였다. 처음엔 뷰 바인딩과 착각했다. 얼마전 과제테스트 연습에서 충격먹고 공부하기로 했던 Live Data 사용에 도움이 될 기능인 것 같다. 이 프로젝트에서는 뷰 바인딩처럼만 사용하였다. [이 게시글](https://dev-imaec.tistory.com/37)과 [개복치님 블로그 글!!](https://philosopher-chan.tistory.com/1308)을 보니 View Model, Live Data와 함께 사용하면 될 것 같다. 
개복치님 블로그 글을 보니 내가 구현했던 전화번호 키패드 앱도 LiveData로 바꿔야 할 것 같다..!
#### build.gradle(:app)
```kotlin 
android {
	(...)
    dataBinding{
        enabled = true
    }
}
```

#### activity_main.xml
크게 `<layout>`태그로 감싸주었다.
```xml
<layout>
    <LinearLayout>
	(...)

    </LinearLayout>
</layout>
```
#### MainActivity.kt
`private lateinit var binding : ActivityMainBinding`
`binding = DataBindingUtil.setContentView(this, R.layout.activity_main)`
`binding.diceStartBtn.setOnClickListener {}`

```kotlin

class MainActivity : AppCompatActivity() {

    private lateinit var binding : ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)

        binding.diceStartBtn.setOnClickListener {
			//클릭 시 실행되는 부분
        }

    }
}
```

## 액션바 없애기, 버튼 색상 바뀌지 않는 현상
#### themes.xml
버튼의 backgroud 색상을 바꿔도 버튼 색상이 바뀌지 않을 때는 `themes.xml` 파일에서  style태그의 parent 값을 `Theme.AppCompat.Light`로 바꾼다.
액션바는 item 태그를 다음과 같이 설정하면 사라진다.

`<style name="Base.Theme.Dice_app" parent="Theme.AppCompat.Light">`
`<item name="windowNoTitle">true</item>`
```
<resources xmlns:tools="http://schemas.android.com/tools">
    <style name="Base.Theme.Dice_app" parent="Theme.AppCompat.Light">
        <item name="windowNoTitle">true</item>
    </style>
    
    <style name="Theme.Dice_app" parent="Base.Theme.Dice_app" />
</resources>
```

## 랜덤 주사위 값 Random.nextInt, when
#### MainActivity.kt
`Random.nextInt(1, 6)` : 1~6의 랜덤 정수
`when(num1){}` : kotlin의 switch문 역할
```kotlin
binding.diceStartBtn.setOnClickListener {

            val num1 = Random.nextInt(1, 6)
            val num2 = Random.nextInt(1, 6)

            if(num1 == num2){
                Toast.makeText(this, "잭팟!", Toast.LENGTH_LONG).show()
            }

            when(num1){
                1 -> diceImage1.setImageResource(R.drawable.dice_1)
                2 -> diceImage1.setImageResource(R.drawable.dice_2)
                3 -> diceImage1.setImageResource(R.drawable.dice_3)
                4 -> diceImage1.setImageResource(R.drawable.dice_4)
                5 -> diceImage1.setImageResource(R.drawable.dice_5)
                else -> diceImage1.setImageResource(R.drawable.dice_6)
            }
            when(num2){
                1 -> diceImage2.setImageResource(R.drawable.dice_1)
                2 -> diceImage2.setImageResource(R.drawable.dice_2)
                3 -> diceImage2.setImageResource(R.drawable.dice_3)
                4 -> diceImage2.setImageResource(R.drawable.dice_4)
                5 -> diceImage2.setImageResource(R.drawable.dice_5)
                else -> diceImage2.setImageResource(R.drawable.dice_6)
            }
        }
```

# 2. 완성 모습
![](https://velog.velcdn.com/images/kuronuma_daisy/post/e4afe873-e3f1-4af6-aaf7-1fded230580e/image.gif)    


# 3. 벨로그에서 보기
[벨로그](https://velog.io/@kuronuma_daisy/Android-%EC%9E%AD%ED%8C%9F-%EC%A3%BC%EC%82%AC%EC%9C%84-%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98with-kotlin)  
