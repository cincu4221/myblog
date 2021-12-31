---
title: 콜백(Callback)함수의 사용법
date: 2021-12-30 17:17:05  
categories: 
- Python

tags:

- Python
- Function
- Callback

---

Plotly 를 사용하여 대시보드를 만드는 동안에 직면했던 여러 문제들중 해결에 꽤 오랜시간이 걸린 문제가 있었다.  
바로 콜백함수에 대한 부분인데 처음보게된 콜백함수가 데코레이터가 적용된 그런 함수였기 때문에 굉장히 헷갈렸다.

## 콜백함수

---
콜백함수란 다른함수의 인자로써 이용되는함수, 어떤 이벤트에 의해 호출되어지는 함수를 말한다.  
함수가 다른함수의 인자로 사용될 수 있다니, 잘 이해가 되지 않을 수 있다.

내가 접했던 콜백함수를 가져와 보면 이렇다.
```python
@app.callback(
    Output('id_fig_age', 'Figure'),
    Input('country-filter', 'value'))
def age_chart_func(value):
    obj = px.bar(data,
                     x=data[data['Q3'] == value]['Q1'][1:].value_counts().sort_index().index,
                     y=data[data['Q3'] == value]['Q1'][1:].value_counts().sort_index().values,
                     )
    obj.update_traces(hovertemplate='%{x}: %{y:.0f}',
                          marker_color='#E08E79',
                          marker_line_width=0,)
    obj.update_layout(paper_bgcolor=colors['content-background'],
                          font_color=colors['text'],
                          plot_bgcolor=colors['plot_background'],
                          autosize=True)
    obj.update_xaxes(title_text='Age Distribution')
    obj.update_yaxes(title_text='Counts')
    return obj
```

전체코드의 일부분이지만 함수를 설명하는데에는 문제가 없다.  

먼저 가장 위에 있는 @app.callback가 무슨뜻인지 이해하지 못한다면 [데코레이터](https://cincu4221.github.io/2021/12/07/Python-Decorator/) 에 대해 간략히 보고 오면 좋다.  
그리고 Output과 Input은 dash.dependencies 라이브러리에서 import 한 것인데, 기능을 살펴보기위해 코드대로 해석하자면  

Input의 괄호안의 첫번째 인자(country-filter)와 ID가 같은 항목을 찾아 두번째 인자(country-filter 의 파라미터 value)를 아래에 있는 함수의 인자로 넣어주며, 인자를 통해 함수를 실행 후 나온 리턴을,  
Output의 괄호안의 첫번째 인자(id_fig_age)와 ID가 같은 항목의 두번째 인자(Figure)로 입력되는 것이다.

위 코드에서 복잡해 보일 수 있는 부분인 px.bar ~ obj.update_yaxes 까지는 그냥 그래프를 그려주는 함수라고 생각하면된다.

이때 이 함수를 모두 실행하고 리턴하는 값인 obj 가 반환되어 Output인 'id_fig_age'의 'Figure'속성으로 입력되고 'id_fig_age'는 함수에서 작성된 그래프를 'Figure'로 갖게되어 화면에 표현해준다.
