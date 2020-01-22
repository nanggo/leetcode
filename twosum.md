# Two Sum


## 문제
양수로 이루어진 배열과 목표값을 입력받는다.
배열에서 두 수를 더해서 목표값이 된다면, 해당하는 인덱스를 리턴해준다.

> 예:
>
> nums = [1, 2, 3, 4], target = 5,
>
> nums[1] + nums[2] = 2 + 3 = 5,
> return [1, 2].

<br>

## 처음 내가 푼 답
최적화를 생각하지 않고 우선은 `brute-force`로 풀었다.
반복문을 중첩했으므로 퍼포먼스에 좋지 않을 것이라 예상했다.

시간 복잡도는 ![O(n^2)](https://user-images.githubusercontent.com/16912219/72887256-ab5d8e00-3d4e-11ea-8b04-d3e21a8cd632.gif)

```javascript
var twoSum = function(nums, target) {
    for(let i = 0, len = nums.length; i < len - 1; i++) {
        for(let j = i + 1; j < len; j++) {
            if(nums[i] + nums[j] === target) return [i, j];
        }
    }
};
```
<br>

## 최적화 되지 않은 결과

![최적화 안된 결과](https://user-images.githubusercontent.com/16912219/72866244-eeebd400-3d1d-11ea-80e9-575a459054bd.png)

역시나 나보다 느린 사람은 18.12%에 없었다.

<br>

## 최적화 해본 답

반복문을 한 번만 이용한다. Map에 key/value로 이뤄진 숫자와 인덱스 값이 저장될 때, value와 더해서 target이 되는 another라는 값이 Map 내에 존재하는지 찾는다.

결과값이 있으면 더 진행하지 않고 해당하는 index들을 `return`한다.

```javascript
var twoSum = function(nums, target) {
  const map = new Map();

  for (let i = 0, len = nums.length; i < len; i++) {
    const another = target - nums[i];

    if (map.has(another)) {
      return [map.get(another), i];
    }
    map.set(nums[i], i);
  }

  return null;
};
```
<br>

## 최적화 결과

Map을 이용해서 key, value로 숫자와 인덱스를 저장했다.
반복문을 한 번 이용했기에 ![O(n)](https://user-images.githubusercontent.com/16912219/72887255-aac4f780-3d4e-11ea-8a67-7333e4b673cd.gif) 복잡도를 갖는다.


![최적화](https://user-images.githubusercontent.com/16912219/72886339-f5de0b00-3d4c-11ea-94e3-300dfc136ccc.png)

최적화 전 속도의 1/3에 지나지 않는다. 메모리를 0.6MB 더 사용하긴 하지만, 유의미한 속도 차이가 나기 때문에 훨씬 나은 결과라고 생각한다.
