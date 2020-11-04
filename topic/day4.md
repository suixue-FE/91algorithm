# 第一题
## 题目描述
给定一个经过编码的字符串，返回它解码后的字符串。

编码规则为: k[encoded_string]，表示其中方括号内部的 encoded_string 正好重复 k 次。注意 k 保证为正整数。

你可以认为输入字符串总是有效的；输入字符串中没有额外的空格，且输入的方括号总是符合格式要求的。

此外，你可以认为原始数据不包含数字，所有的数字只表示重复的次数 k ，例如不会出现像 3a 或 2[4] 的输入。


示例 1：

输入：s = "3[a]2[bc]"
输出："aaabcbc"

示例 2：
输入：s = "3[a2[c]]"
输出："accaccacc"

示例 3：
输入：s = "2[abc]3[cd]ef"
输出："abcabccdcdcdef"

示例 4：
输入：s = "abc3[cd]xyz"
输出："abccdcdcdxyz"

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/decode-string
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

[前往答题](https://github.com/leetcode-pp/91alg-2/issues/21)

## 个人解答

**思路:**

1. 见到括号字符串就用栈，一般见到`[`就入栈，见到`]`就出栈
2. 数字、'`[`'、字母、'`]`'四种情况
3. 见到数字使用num缓存
4. 见到`[`入栈，记得把缓存的数字入栈之后清空
5. 字母直接入栈
5. 见到`]`出栈知道看到之前入栈的`[`，此时是一套字母，然后再把栈顶的数字拿出来×字符串

**代码:**
javascript
``` javascript
/**
 * @param {string} s
 * @return {string}
 */
var decodeString = function(s) {
  let stack =[],len = s.length,num = 0
  for (let i = 0; i < len; i++) {
    const n = s[i];
    if (!isNaN(n)) {
      num= Number(num*10) + Number(n)
    }
    else if (n==']'){
      let str = '',string = ''
      // console.log(stack);
      while (stack.length && stack[stack.length-1]!=='['){
        str=`${stack.pop()}${str}`
      }
      string = str
      if (stack[stack.length-1]=='[') {
        stack.pop()
        let number = stack.pop()
        while(number-1>0){
          string = `${string}${str}`
          number--
        }
        // string = string.repeat(number) // 虽然简单但是居然慢！
      }
      stack.push(string)
    }else if(n=='['){
      stack.push(num)
      stack.push(n)
      num=0
    }else stack.push(n)
  }
  
  return stack.join('')
};
```

**复杂度分析:**
n为数组长度
时间复杂度：O(n)
空间复杂度：O(n)

**模板：** 无 
