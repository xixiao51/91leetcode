### 思路

从最后一位开始模拟加法进位计算， 注意不可以直接转化成数字相加会溢出 - Integer

### 代码


```java

class Solution {
    public List<Integer> addToArrayForm(int[] num, int k) {
        List<Integer> result = new ArrayList<>();
        int len = num.length - 1;
        //先将最后一位加入list，此时list为倒序
        int sum = num[len] + k;
        result.add(sum % 10);
        int carry = sum / 10;
        
        //从倒数第二位开始循环
        for(int i = len - 1; i >= 0; i--) {
            sum = num[i] + carry;
            result.add(sum % 10);
            carry = sum / 10;
        }
        
        //如果carry还有进位
        while(carry > 0) {
            result.add(carry % 10);
            carry /= 10;
        }
        
        //反转数组
        Collections.reverse(result);
        return result;
    }
}


```

**复杂度分析**
- 时间复杂度：O(max(N, log k))，其中 N 为数组num长度。
- 空间复杂度：O(max(N, log k)), 储存结果的新数组
