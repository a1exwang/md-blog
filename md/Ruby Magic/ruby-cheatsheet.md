# Ruby Cheatsheet

- tags: ruby, cheatsheet, one-line script

------

- `Array` Class
  - `new`, 创建指定个数元素的数组
    - `Array.new(4) { |x| i*i }  # => [1, 4, 9, 16]`
  - `[]`, 元素和子数组

        arr = [1, 2, 3, 4, 5, 6]
        arr[2]    #=> 3
        arr[100]  #=> nil
        arr[-3]   #=> 4
        arr[2, 3] #=> [3, 4, 5]
        arr[1..4] #=> [2, 3, 4, 5]
        arr[1..-3] #=> [2, 3, 4]

  - `uniq`, 去重
  - `select`, `reject`, 过滤

        arr.select { |a| a > 3 }     #=> [4, 5, 6]
        arr.reject { |a| a < 3 }     #=> [3, 4, 5, 6]

  - `<<`, `push`, `insert`

        arr.insert(3, 'apple')  #=> [0, 1, 2, 'apple', 3, 4, 5, 6]
        arr.push('fuck')
        arr << 'fuck'
        # <<是push的别名

  - `collect`, `map`
  - `inject`, `reduce`
  - `size`, `length`, `count`
    - `size`, `length`: 获取数组元素个数
    - `count`: 数出满足条件的元素个数, 如果没有参数等价于`size`
  - `shuffle`, `sample`, 随机
    - `shuffle`, 打乱顺序
    - `sample(n)`, 抽出n个元素, 返回元素最多等于数组元素个数
  - `sort`, `sort_by`排序
    - `sort { |x,y| x <=> y }`: 传入的block是比较器
    - `sort_by { |x| x.size }`: 传入的是映射函数f, 将数组元素按照函数f映射后的值排序.
  - `|`, `&`, '+', '-': 逻辑运算

- `String` Class
  - `%`: 类似于printf的格式化

        "%05d" % 123                              #=> "00123"
        "%-5s: %08x" % [ "ID", self.object_id ]   #=> "ID   : 200e14d6"
        "foo = %{foo}" % { :foo => 'bar' }        #=> "foo = bar"

  - `each_char`, `each_byte`, `each_line`
  - `capitalize`, `downcase`, `upcase`
  - `center`

        "hello".center(4)         #=> "hello"
        "hello".center(20)        #=> "       hello        "
        "hello".center(20, '123') #=> "1231231hello12312312"

  - `encoding`, `force_encoding(encoding)`, `encode(encoding)`
    - `force_encoding(encoding)`: 强行把一个字符串当成另一种encoding来解析
    - `encode(encoding)`: 转换编码格式到encoding
  - `gsub(pattern, replacent)`
    - 正则表达式替换
  - `replace(str)`
    - 替换self中的字符串成为str(拷贝构造)
  - `intern`, `to_sym`: 转换为Symbol
  - `strip`

        "    hello    ".strip   #=> "hello"
        "\tgoodbye\r\n".strip   #=> "goodbye"
  - `succ`

        "abcd".succ        #=> "abce"
        "THX1138".succ     #=> "THX1139"
        "<<koala>>".succ   #=> "<<koalb>>"
        "1999zzz".succ     #=> "2000aaa"
        "ZZZ9999".succ     #=> "AAAA0000"
        "***".succ         #=> "**+"
  - `unpack(format) → anArray`
    - 将字符串中的数据转换为数组

- `Hash` Class
  - `invert`: 反转key和value
  - `key(value)`: 通过value获取key
  - `merge(hash)`: 合并, hash和self有共同的key则取hash的value

- `Kernel` Class
- `Regexp` Class
