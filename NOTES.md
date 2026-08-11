- (self, other)는 그냥 튜플 하나
def __init__(self, data, _children=(), _op='', label=''):
에서 __init__이 받는 위치 인자는 두 개 -> data와 _children

그래서 Value(self.data + other.data, (self, other))는 
첫 번째 인자 -> 계산된 숫자
두 번째 인자 -> (self, other)는 원소가 2개인 튜플 하나

- _children=()은 기본값이 빈 튜플
a = Value(2.0) -> _children이 안넘어오므로 self._prev은 빈 집합

- set(_children)으로 바꾸는 이유
self._prev = set(_children)은 튜플 -> 집합 변환으로 _children(a, a)는 {a}로 변환
같은 노드가 두 번 들어와도 그래프상 부모 노드는 하나면 됨

- local gradient만 쓰고 upstream 곱하는 걸 빼먹음
grad = 부모 grad * local

- .data는 값, .grad는 그 값이 L에 주는 영향(dL/d해당값)

- backprop은 결국 chain rule (dy/dx = dy/du * du/dx)를 이용하는 것

- gradient 계산할 때, f(x+h) - f(x) / h 활용하여 교차 검증